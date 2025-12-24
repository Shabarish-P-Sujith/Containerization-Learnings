# DOCKER HUB

## Pushing Images (push a new image to the repository using the CLI) :-

## KEY POINT : 
Always include <username>/ before the repository name when tagging and pushing the images to Docker Hub !! 

## COMMANDS:

1. Log in to Docker Hub.
```bash
docker login
```
- You should log in before pushing to a registry that requires authentication. 
- This is the standard first step.

---

2. Build the Docker Image (only if the image is NOT already present locally).
```bash
docker build -t <local-image>:<local-tag> .
```
- This is correct if you need to build the image locally. 
- If the image already exists locally, you can skip the build step and move to tagging/pushing.

---

3. Tag the local image with the Docker Hub repository name.
```bash
docker tag <local-image>:<local-tag> <username>/<new-docker-repo>:<tagname>
```
- This is the typical way to rename or re-tag a locally built image for a target registry/repo. 

---

4. Push the image to Docker Hub.
```bash
docker push <username>/<new-docker-repo>:<tagname>
```
- Correct for uploading the tagged image to the registry you logged into (Docker Hub or another registry).

---

5. Pull the image from Docker Hub. (-- OPTIONAL --)
```bash
docker pull <username>/<new-docker-repo>:<tagname>
```
- This is unnecessary immediately after pushing if your goal is to push.
- You would pull only if you need to fetch the image from the registry to another host or verify visibility.

--- 

6. Log out from Docker Hub (-- OPTIONAL --).
```bash
docker logout   
```
- Logging out is optional.
- Do it if you want to remove credentials from the local environment or when done with a shared system.