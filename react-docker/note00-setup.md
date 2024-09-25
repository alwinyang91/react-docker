

# 0. Create a new repository `react-docker` in GitHub

# 1. Create a React application locally
```zsh
mkdir react-docker
cd react-docker
npm create vite@latest .
code .
```
- Select a framework: React
- Select a variant: TypeScript

> Note: we do not run `npm install` or `npm run dev`.
> Because all the installation and dependencies will be installed within dockerized container.

# 2. Push to GitHub
```zsh
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:alwinyang91/react-docker.git
git push -u origin main
```

