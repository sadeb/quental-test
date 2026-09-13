FROM nexus.countigo.org:5000/node:24.19.0-alpine AS build
WORKDIR /workspace
COPY package.json package-lock.json ./
RUN npm ci
COPY . .
RUN npm run build

FROM nexus.countigo.org:5000/nginx:1.29.1-alpine
COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build /workspace/dist/rick-morty/browser /usr/share/nginx/html
EXPOSE 80
