FROM node:22-alpine

# create a user with permissions to run the app
# -S -> create a system user
# -G -> add the user to a group
# This is done to avoid running the app as root
# If the app is run as root, any vulnerability in the app can be exploited to gain access to the host system
# It's a good practice to run the app as a non-root user
# Create a group and a system user
# A group called appgroup.
# A system user called appuser and assigns them to appgroup.
RUN addgroup appgroup && adduser -S -G appgroup appuser

# set the user to run the app
USER appuser

# set the working directory to /app
WORKDIR /app

# copy package.json and package-lock.json to the working directory
# This is done before copying the rest of the files to take advantage of Docker’s cache
# If the package.json and package-lock.json files haven’t changed, Docker will use the cached dependencies
COPY package*.json ./

# sometimes the ownership of the files in the working directory is changed to root
# and thus the app can't access the files and throws an error -> EACCES: permission denied
# to avoid this, change the ownership of the files to the root user
USER root

# chown -R <user>:<group> <directory>
# chown command changes the user and/or group ownership of for given file.
# Change the ownership of the /app directory to the app user and group
RUN chown -R appuser:appgroup .

# change the user back to the app user
USER appuser

# install dependencies
RUN npm install

# copy the rest of the files to the working directory
COPY . .

# expose port 5173 to tell Docker that the container listens on the specified network ports at runtime
EXPOSE 5173

# command to run the app
CMD ["npm", "run", "dev"]