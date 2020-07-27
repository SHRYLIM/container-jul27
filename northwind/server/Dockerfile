# this image will be based on Node v14
FROM node:14

# environment variable to define my workspace
ENV APP_DIR=/app APP_PORT=3000 

# far database
DB_USER=root DB_PASSWORD=changeit

# create and cd into APP_DIR
WORKDIR ${APP_DIR}

# copy the files 
ADD main.js .
ADD package.json .
ADD package-lock.json .

# copy the directories
ADD config config
ADD public public
ADD views views

# install the dependencies - package.json
RUN npm install

# add healthcheck
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \ 
    CMD curl -s -f http://localhost:{APP_PORT}/health || exit 1

# expose the port
EXPOSE ${APP_PORT}

# run the application 
ENTRYPOINT ["node","main.js"]