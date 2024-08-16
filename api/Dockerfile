FROM node:19-alpine
WORKDIR /src
COPY package.json package-lock.json /src/
RUN npm config set strict-ssl false
RUN npm install
COPY . .
EXPOSE 80
CMD ["npm", "run", "serve"]