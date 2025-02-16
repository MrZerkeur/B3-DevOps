FROM node:alpine
WORKDIR /app
RUN adduser -D user
COPY package.json .
RUN npm install
COPY index.ts .env ./
RUN npx tsc index.ts
USER user
CMD ["node", "index.js"]