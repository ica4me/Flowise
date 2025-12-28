# Flowise Docker Hub Image

Start Flowise using the [DockerHub Image](https://hub.docker.com/r/flowiseai/flowise).

## Usage

1. Create a `.env` file in the same directory. You can copy the configuration below:

   ```ini
   PORT=3000
   SECRETKEY_PATH=/root/.flowise

   LOG_PATH=/root/.flowise/logs

   TOOL_FUNCTION_BUILTIN_DEP=crypto,fs,path
   TOOL_FUNCTION_EXTERNAL_DEP=mysql2,moment,lodash,axios,cheerio
   ALLOW_BUILTIN_DEP=true

   BLOB_STORAGE_PATH=/root/.flowise/storage

   CORS_ORIGINS=*
   IFRAME_ORIGINS=*
   FLOWISE_FILE_SIZE_LIMIT=500mb

   JWT_AUTH_TOKEN_SECRET='AABBCCDDAABBCCDDAABBCCDDAABBCCDDAABBCCDD'
   JWT_REFRESH_TOKEN_SECRET='AABBCCDDAABBCCDDAABBCCDDAABBCCDDAABBCCDD'
   JWT_ISSUER='ISSUER'
   JWT_AUDIENCE='AUDIENCE'
   JWT_TOKEN_EXPIRY_IN_MINUTES=360
   JWT_REFRESH_TOKEN_EXPIRY_IN_MINUTES=43200
   
2. `docker compose up -d`
4. Open [http://localhost:3000](http://localhost:3000)
5. You can bring the containers down by `docker compose stop`

## 🌱 Env Variables

If you like to persist your data (flows, logs, credentials, storage), set these variables in the `.env` file inside `docker` folder:

-   DATABASE_PATH=/root/.flowise
-   LOG_PATH=/root/.flowise/logs
-   SECRETKEY_PATH=/root/.flowise
-   BLOB_STORAGE_PATH=/root/.flowise/storage

Flowise also support different environment variables to configure your instance. Read [more](https://docs.flowiseai.com/configuration/environment-variables)

## Queue Mode:

### Building from source:

You can build the images for worker and main from scratch with:

```
docker compose -f docker-compose-queue-source.yml up -d
```

Monitor Health:

```
docker compose -f docker-compose-queue-source.yml ps
```

### From pre-built images:

You can also use the pre-built images:

```
docker compose -f docker-compose-queue-prebuilt.yml up -d
```

Monitor Health:

```
docker compose -f docker-compose-queue-prebuilt.yml ps
```
