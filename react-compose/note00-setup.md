
---
---
# 1. Create a React application locally
```zsh
cd react-docker
npm create vite@latest react-compose
```
- Select a framework: React
- Select a variant: TypeScript

> Note: we do not run `npm install` or `npm run dev`.
> Because all the installation and dependencies will be installed within dockerized container.

# 2. Use docker init
```zsh
cd react-compose
docker init
```
- platform: Node
- version: 20
- package manager: npm
- npm run build: No
- start the app: npm run dev
- port: 5173

# 3. Modification
- replace the Dockerfile
- rename the server to web
```yaml
services:
  web:
    build:
      context: .
    environment:
      NODE_ENV: production
    ports:
      - 5173:5173
```
- remove the environment variable and make volume variables
```yaml
services:
  web:
    build:
      context: .
    ports:
      - 5173:5173
    volumes:
      - .:/app
      - /app/node_modules
```

- add --host to package.json
```zsh
docker compose up
```

