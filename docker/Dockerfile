# Stage 1: Build stage
FROM node:20-alpine AS build

USER root

# Skip downloading Chrome for Puppeteer (saves build time)
ENV PUPPETEER_SKIP_DOWNLOAD=true

# Install latest Flowise globally
RUN npm install -g flowise

# Stage 2: Runtime stage
FROM node:20-alpine

# Install runtime dependencies
# Menambahkan python3, make, g++ agar support install library berat
RUN apk add --no-cache chromium git python3 py3-pip make g++ build-base cairo-dev pango-dev curl

# Set the environment variable for Puppeteer to find Chromium
ENV PUPPETEER_EXECUTABLE_PATH=/usr/bin/chromium-browser

# Copy Flowise from the build stage
COPY --from=build /usr/local/lib/node_modules /usr/local/lib/node_modules
COPY --from=build /usr/local/bin /usr/local/bin

# --- BAGIAN PENTING YANG DITAMBAHKAN ---
# Install library tambahan secara permanen (mysql2, dll)
# Ini yang memperbaiki error "Cannot find module 'mysql2/promise'"
RUN npm install -g mysql2 pg axios cheerio moment

# Pastikan Node.js tahu di mana mencari modul global ini
ENV NODE_PATH=/usr/local/lib/node_modules

# Kembali ke pengaturan awal untuk menjalankan Flowise
ENTRYPOINT ["flowise", "start"]