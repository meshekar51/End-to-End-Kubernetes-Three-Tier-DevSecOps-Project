
# Stage 1: Build frontend
FROM dhi.io/node:24-dev AS build

WORKDIR /usr/src/app

# Files are relative to the Docker build context
COPY package.json ./
RUN npm install --package-lock-only && npm ci

RUN npm ci

COPY . .

RUN npm run build

RUN npm prune --omit=dev

# Stage 2: Production
FROM dhi.io/node:24

WORKDIR /app

COPY --from=build /usr/src/app/build ./build
COPY --from=build /usr/src/app/node_modules ./node_modules
COPY --from=build /usr/src/app/package.json ./

EXPOSE 3000

# Adjust for your actual application entry point
CMD ["node", "build/index.js"]
