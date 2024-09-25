
---
---
# 1. Sycnize the local directory to the container directory
```zsh
cd react-docker
docker run -p 5173:5173 -v "$(pwd):/app" -v /app/node_modules react-docker:v0.2
```
- `-v "$(pwd):/app"`: This mounts your local directory (where your project files like package.json reside) into the container’s /app directory.
- `-v /app/node_modules`: This creates an anonymous volume for the /app/node_modules directory inside the container.

As a result, the node_modules inside the container is not shared with your local machine. It exists only inside the container, 
and any changes to dependencies inside the container won’t affect your local node_modules.

However, we did not install the packages, we do not have the node_modules, so `-v /app/node_modules` is necessary.

Otherwise, it will show `sh: vite: not found`, due to that If node_modules is not available in the container, Vite won't be found.

# 2. Test the synchronization
If you change react-docker/src/App.tsx, locally. The container files will be synced.
```tsx
<h1>Vite + React is awosome! </h1>
```