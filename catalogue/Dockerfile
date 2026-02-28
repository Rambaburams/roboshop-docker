from node:20.20.0-alpine3.23 AS build
workdir /opt/server
copy package.json .
copy *.js .
RUN npm install 

FROM node:20.20.0-alpine3.23 
RUN addgroup  -S roboshop && adduser -S roboshop -G roboshop
workdir /opt/server
COPY --from=build /opt/server /opt/server
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"
RUN chown -R roboshop:roboshop /opt/server
USER roboshop

CMD ["node", "server.js"]