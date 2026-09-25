# MinIO Deployment Documentation

## Deployment Method

For me, MinIO was deployed using a Docker container within the KillerCoda Ubuntu environment. Utilizing Docker in the installation process by eliminating the need to manually configure the MinIO server and its required dependencies.

## Docker Command

The following command was used to launch the MinIO container:

```bash
docker run -d -p 9000:9000 -p 9001:9001 --name minio-server \
-e "MINIO_ROOT_USER=cloudadmin" \
-e "MINIO_ROOT_PASSWORD=CloudNova2026!" \
quay.io/minio/minio server /data --console-address ":9001"
```

## Port Configuration

Two ports were exposed during deployment:

* **Port 9000** – Used for the MinIO API
* **Port 9001** – Used for the MinIO Web Console

The web-based admin interface can be accessed through port **9001**.

## Administrator Credentials

The administrator account was set through environment variables in the Docker command:

* **Username:** `cloudadmin`
* **Password:** `CloudNova2026!`

## Environment Variables

The `-e` flags in the Docker command were used to define configuration settings for the container:

* `MINIO_ROOT_USER=cloudadmin`

  * Sets the root administrator username

* `MINIO_ROOT_PASSWORD=CloudNova2026!`

  * Sets the root administrator password

## Object Storage Bucket

A bucket named:

```
client-photos
```

was created using the MinIO Web Console.

To verify functionality, a test file was uploaded successfully to confirm that object storage is working as expected.

## Container Verification

To ensure that the MinIO container is running properly, the following command was executed:

```bash
docker ps
```

The output confirmed that the container is active and that the required ports are correctly mapped.
