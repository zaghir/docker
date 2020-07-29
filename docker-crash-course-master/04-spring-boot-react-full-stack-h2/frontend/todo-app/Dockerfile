## Stage 1 - Lets build the "deployable package"
FROM node:8.10 as frontend-build
RUN mkdir -p /fullstack/frontend && chown -R node:node /fullstack/frontend
WORKDIR /fullstack/frontend

# Step 1 - Download all package dependencies first.
# We will redownload dependencies only when packages change.
COPY package.json package-lock.json ./
USER node
RUN npm install

# Step 2 - Copy all source and run build
COPY . ./
RUN npm run build



## Stage 2 - Let's build a minimal image with the "deployable package"
FROM nginx:1.12-alpine
COPY --from=frontend-build /fullstack/frontend/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

# frontend-build  ==> FROM node:7.10 as frontend-build   , give a name off image and get build application 
# daemon off; ==> run nginx as main proccess not like background proccess => daemon off


# build image with command , in the root folder  (frontend/todo-app)
# docker build .