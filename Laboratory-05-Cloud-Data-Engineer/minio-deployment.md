# MinIO Deployment Documentation

## Deployment Method

As an IT, for me the MinIO was set up using a Docker container inside the KillerCoda Ubuntu environment. By using Docker, the deployment process became simpler since there was no need to manually install or configure the MinIO server along with its dependencies.

## Docker Command

The command below was used to start the MinIO container:

```bash
docker run -d -p 9000:9000 -p 9001:9001 --name minio-server \
-e "MINIO_ROOT_USER=cloudadmin" \
-e "MINIO_ROOT_PASSWORD=CloudNova2026!" \
quay.io/minio/minio server /data --console-address ":9001"
```

## Port Configuration

During deployment, two ports were exposed:

* **Port 9000** – Handles the MinIO API
* **Port 9001** – Provides access to the MinIO Web Console

The administrative web interface can be opened through port **9001**.

## Administrator Credentials

The admin account was defined using environment variables in the Docker command:

* **Username:** `cloudadmin`
* **Password:** `CloudNova2026!`

## Environment Variables

The `-e` options in the Docker command were used to configure the container:

* `MINIO_ROOT_USER=cloudadmin`

  * Specifies the root administrator username

* `MINIO_ROOT_PASSWORD=CloudNova2026!`

  * Specifies the root administrator password

## Object Storage Bucket

A bucket named:

```
client-photos
```

was created through the MinIO Web Console.

A sample file was uploaded to confirm that the object storage system is functioning correctly.

## Container Verification

To verify that the MinIO container is running, the following command was used:

```bash
docker ps
```

The result showed that the container is active and the ports are properly mapped.
