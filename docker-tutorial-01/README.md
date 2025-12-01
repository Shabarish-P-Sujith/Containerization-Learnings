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
--- "OR" ---
RUN nom ci

- Install all project dependencies inside the image.

- 'npm install' : 
    - modifies package-lock.json if needed
    - installs dependencies based on package.json
    - for development and adding/updating packages.

- 'npm ci' : 
    - requires a package-lock.json
    - optimized for CI/CD
    - for automated builds and production for speed and consistency

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

# TERMINAL COMMAND
```bash
docker build -t react-img-01:v1 .

docker run -d -p 3000:5173 react-img-01:v1
```

## NOTE

- Development / Debugging             → no -d, just -p

- Normal run / Background service     → use -d