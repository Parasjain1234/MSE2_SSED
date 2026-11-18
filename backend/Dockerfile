FROM node:20-alpine3.20

WORKDIR /app

ENV NODE_ENV=production

COPY package.json package-lock.json* ./
RUN npm ci --omit=dev

COPY src ./src
COPY db ./db

USER 1000:1000

EXPOSE 3000

HEALTHCHECK --interval=10s --timeout=3s --start-period=10s --retries=10 \
  CMD ["node", "-e", "fetch('http://localhost:3000/health').then(r=>{if(!r.ok)process.exit(1)}).catch(()=>process.exit(1))"]

CMD ["npm", "start"]