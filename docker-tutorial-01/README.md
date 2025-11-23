This is the standard + correct + professional sequence for Node/Vite development Dockerfiles, which should be done accordingly. (the same steps should be followed)

# EXPLANATION

FROM node:24-alpine

- Use Node.js 24 (lightweight version) as the BASE for the container.

WORKDIR /app

- Create a folder called /app inside the container and work inside it.
- Used to mention the Working Directory

COPY package.json ./*

- Copy package.json + package-lock.json into /app (Used to install dependencies)

RUN npm install

- Install all project dependencies inside the image.

COPY . .

- Copy your whole project into the container's /app folder.
- 1st dot is for current folder/file --> Dockerfile
- 2nd dot is for the container --> '/app'

EXPOSE 5173

- Tell Docker that this app uses port 5173 (Vite's port).

CMD ["npm", "run", "dev", "--", "--host"]

- When the container starts → run the development server AND allow external access.


## NOTE

- RUN = Executes Commands at Build-time (this is Image Level)
- CMD = Executes Commands at Run-time   (this is Container Level)