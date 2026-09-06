# Dockerfile patterns

## Multi-stage Node.js example
```dockerfile
# Build stage
FROM node:20-slim AS build
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm ci
COPY . .
RUN npm run build

# Runtime stage
FROM node:20-slim
WORKDIR /app
RUN useradd --system --create-home appuser
COPY --from=build /app/dist ./dist
COPY --from=build /app/node_modules ./node_modules
USER appuser
EXPOSE 3000
CMD ["node", "dist/index.js"]
```

## Multi-stage Python example
```dockerfile
FROM python:3.12-slim AS build
WORKDIR /app
COPY requirements.txt .
RUN pip install --user --no-cache-dir -r requirements.txt

FROM python:3.12-slim
WORKDIR /app
RUN useradd --system --create-home appuser
COPY --from=build /root/.local /home/appuser/.local
COPY . .
USER appuser
ENV PATH=/home/appuser/.local/bin:$PATH
CMD ["python", "app.py"]
```

## docker-compose for local multi-service dev
```yaml
services:
  app:
    build: .
    ports: ["3000:3000"]
    environment:
      DATABASE_URL: postgres://user:pass@db:5432/appdb
    depends_on: [db]
  db:
    image: postgres:16-alpine
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: pass
      POSTGRES_DB: appdb
    volumes:
      - db-data:/var/lib/postgresql/data
volumes:
  db-data:
```
Note: real secrets (DB passwords, API keys) shouldn't be hardcoded even in local compose files if the repo is ever going to be shared — use a `.env` file excluded via `.gitignore`, referenced with `${VAR_NAME}` syntax.
