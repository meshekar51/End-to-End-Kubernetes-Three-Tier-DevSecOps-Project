# Stage 1: Build
FROM dhi.io/node:24-dev AS build

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm ci

COPY . .

RUN npm run build

# Remove development dependencies
RUN npm prune --omit=dev


# Stage 2: Production
FROM dhi.io/node:24

WORKDIR /app

COPY --from=build /usr/src/app/build ./build
COPY --from=build /usr/src/app/node_modules ./node_modules
COPY --from=build /usr/src/app/package*.json ./

EXPOSE 3000

# Adjust this to your application's actual entry point
CMD ["node", "build/index.js"]
