# MongoDB backup

[![Build Status](https://travis-ci.org/neo9/mongodb-backups.svg?branch=master)](https://travis-ci.org/neo9/mongodb-backups)


Create MongoDB snapshots to an encrypted S3 bucket.
Handle snapshot restoration from backup.
Can be easily monitored by Prometheus.

[Docker repository](https://hub.docker.com/r/neo9sas/mongodb-backups)

## Usage

```bash
# Launch server & scheduler
./mongodb-backups --config ./config.yaml
# List backup
./mongodb-backups --config ./config.yaml --list
# Restore specific backup
./mongodb-backups --config ./config.yaml --restore [id] --args '--drop'
# Restore last backup
./mongodb-backups --config ./config.yaml --restore-last --args '--drop'
```

Parameters:

- `--config`: Config path. Default `./config.yaml`
- `--list`: list backups
- `--restore`: Restore specific backup from snapshot
- `--restore-last`: Restore last backup from snaphost
- `--args`: MongoDB restore additional arguments

## TODO

- Prometheus alerts example

## Config file

- `name`: backup name
- `schedule`: cronJob schedule. Example: `0 * * * *`
- `mongodb`:
    - `host`: MongoDB host
    - `port`: MongoDB port
- `bucket`: dictionary
    - `s3`:
        - `name`: bucket name
        - `region`: bucket region


## Environment variables

- `MONGODB_USER`: MongoDB user
- `MONGODB_PASSWORD`: MongoDB password

## Development

### Run

```bash
# With Go
go run ./cmd --config config.yaml

# With Docker
docker build -t n9-backup .
docker run --rm -v /tmp/config:/tmp/config n9-backup mongodb-backup --config /tmp/config/config.yaml
```

