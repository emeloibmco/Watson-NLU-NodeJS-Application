FROM node:12-alpine AS builder
WORKDIR /app
COPY . .
RUN npm install && npm run build
FROM node:12-alpine
RUN npm install -g serve
COPY --from=builder app/dist/crashapp /app
EXPOSE 6001
ENTRYPOINT ["serve", "-l", "6001", "/app"]