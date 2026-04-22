FROM node:18-alpine

WORKDIR /app

# 🔥 CRITICAL: update system packages
RUN apk update && apk upgrade

COPY app/package*.json ./

RUN npm install --only=production

COPY app/ .

RUN addgroup -S appgroup && adduser -S appuser -G appgroup

USER appuser

EXPOSE 3000

CMD ["node", "app.js"]