FROM node:8-alpine

COPY ./package.json /packages/package.json
RUN cd /packages/ && npm install -q

WORKDIR /personal_website

RUN cp -a /packages/* /personal_website/
COPY . /personal_website

EXPOSE 8080

CMD ["node_modules/.bin/http-server", "public", "-p 8080"]