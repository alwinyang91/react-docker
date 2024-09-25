
---
---
# 1. Use docker watch function
```yaml
# specify the version of docker-compose
version: "3.8"

# define the services/containers to be run
services:
  # define the frontend service
  # we can use any name for the service. A standard naming convention is to use "web" for the frontend
  web:
    # # we use depends_on to specify that service depends on another service
    # # in this case, we specify that the web depends on the api service
    # # this means that the api service will be started before the web service
    # depends_on: 
    #   - api

    # specify the build context for the web service
    # this is the directory where the Dockerfile for the web service is located
    build:
      context: .

    # specify the ports to expose for the web service
    # the first number is the port on the host machine
    # the second number is the port inside the container
    ports:
      - 5173:5173

    # specify the environment variables for the web service
    # these environment variables will be available inside the container
    environment:
      VITE_API_URL: http://localhost:8000

    # this is for docker compose watch mode
    # anything mentioned under develop will be watched for changes by docker compose watch and it will perform the action mentioned
    develop:
      # we specify the files to watch for changes
      watch:
        # it'll watch for changes in package.json and package-lock.json and rebuild the container if there are any changes
        - path: ./package.json
          action: rebuild
        - path: ./package-lock.json
          action: rebuild
        # it'll watch for changes in the frontend directory and sync the changes with the container real time
        - path: .
          target: /app
          action: sync

```

Then 
```zsh
docker compose up
docker compose watch
```