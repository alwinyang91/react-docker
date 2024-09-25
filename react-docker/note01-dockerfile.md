
---
---
# 1. Create a Dockerfile
```zsh
cd react-docker
touch Dockerfile
```
# 2. Create a dockerignore file
```zsh
cd react-docker
touch ".dockerignore"
```

# 3. Build the image
```zsh
cd react-docker
docker build -t react-docker:v0.1 .
```
- `-t, --tag`: Name and optionally a tag in the `name:tag` format
- `.`: the current directory


# 4. Run the docker image
```zsh
docker run -p 5173:5173 react-docker:v0.1
```
> Note: This does not work, because the network is not exposed.

In the package.json file, add --host to the vite
```json
  "scripts": {
    "dev": "vite --host",
```

# 5. Rebuild the image
```zsh
docker build -t react-docker:v0.2 .
docker run -p 5173:5173 react-docker:v0.2
```

