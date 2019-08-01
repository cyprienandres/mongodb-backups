# MongoDB backup

[![Build Status](https://travis-ci.org/neo9/mongodb-backups.svg?branch=master)](https://travis-ci.org/neo9/mongodb-backups)


Backup MongoDB dumps to S3 or GCS.

## Usage

```bash
./mongobackup --config ./config.yaml
```

## TODO

- Prometheus metrics and alerting

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

