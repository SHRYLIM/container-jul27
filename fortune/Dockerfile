# the environment
# this image will be based on Node v14
FROM node:14

## building the image
# environment variable to define my workspace
# 3000 is the port that the application is going to listen to
# create new dir so if there is problem with image, know where to look
# can change variables easily without changing rest of the code 
ENV APP_DIR=/app APP_PORT=3000

# create and cd into APP_DIR
# mkdir /app
# cd /app
WORKDIR ${APP_DIR}

# copy the file from fortune into /app
# ADD local image
# copy the files
ADD main.js .
ADD package.json .
ADD package-lock.json . 
# copy the directories
ADD public public
ADD views views

# install the dependencies - package.json
RUN npm install

## running the image
# add healthcheck
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
    CMD curl -s -f http://localhost:{APP_PORT}/health || exit 1
# the port the application is exposing
EXPOSE ${APP_PORT}

# run the application
ENTRYPOINT [ "node", "main.js" ]