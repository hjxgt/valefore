FROM stackupiss/northwind-app:v1

## Building the application
# create a directory /app and cd into it
WORKDIR /app

ADD main.js .
ADD package.json .
ADD package-lock.json .
ADD views views
ADD public public

# node_modules
RUN npm ci

# run app & set env value
ENV PORT=5000 
ENV INSTANCE_NAME=dovbear1
ENV HEROKU_WORKAROUND=true

# health check
HEALTHCHECK --interval=30s --timeout=10s --start-period=5s --retries=3 CMD curl -s http://localhost:${APP_PORT}/healthz || exit 1

# what port does the application bind to
EXPOSE ${PORT}

# start the application
ENTRYPOINT node main.js
