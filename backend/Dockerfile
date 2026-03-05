# --- STAGE 1: Builder ---
FROM node:20-alpine AS builder

WORKDIR /app

# Install system dependencies for Prisma and compilation
RUN apk add --no-cache openssl libc6-compat

COPY package*.json ./
RUN npm install

# Copy source and generate Prisma Client
COPY . .
RUN npx prisma generate
RUN npm run build

# Remove development dependencies to keep the image slim and secure
RUN npm prune --production

# --- STAGE 2: Production Runner ---
FROM node:20-alpine AS runner

WORKDIR /app

# Install only necessary runtime libraries
RUN apk add --no-cache openssl libc6-compat

# Security Best Practice: Use a non-root user
# Node images come with a 'node' user by default
USER node

# Copy only the necessary files from builder
COPY --from=builder --chown=node:node /app/dist ./dist
COPY --from=builder --chown=node:node /app/node_modules ./node_modules
COPY --from=builder --chown=node:node /app/package*.json ./
COPY --from=builder --chown=node:node /app/prisma ./prisma

ENV NODE_ENV=production
EXPOSE 3000

# Using 'node' directly instead of 'npm' for better signal handling (PID 1)
CMD ["node", "dist/src/main"]