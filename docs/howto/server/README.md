#mole-server

The mole-server is built in go and uses mongodb as database. Once both are installed on your stack,
do:


## Install

```
go get https://github.com/molejs/mole-server
```

## Configure and run

Configuration of mole server is done via environment variables.

| Name              | Description                    | Default value
| ----------------- | ------------------------------ | ------------------
| `MOLE_ADDR`       | Server address, e.g `:8080`    | `:8080`
| `MOLE_MONGO_ADDR` | MongoDB server address         | `127.0.0.1:27017`
| `MOLE_DB_NAME`    | MongoDB database name for mole | `127.0.0.1:27017`
| `MOLE_KEY`        | SSL certificate key            | none [1]
| `MOLE_CERT`       | SSL certificate                | none [1]

[1] If cert and key are not empty the server will be started as an HTTPS server.

To run the server just:
```
go run server.go
```

## Retrieving logs
```bash
curl http://example.com/logs?limit=20&skip=0
```
**Query string params**

| Param name | Description                       | Required | Default value
| ---------- | --------------------------------- | -------- | --------------
| `limit`    | Max number of logs to retrieve    | no       | `25`
| `skip`     | Skip first n logs when retrieving | no       | `0`

All results are ordered by descending creation date.
A successful result looks like:
```json
{
  "error": false,
  "logs": [array of logs]
  "count": 10, // The number of logs retrieved
  "total": 50 // Total number of logs
}
```

## Reporting logs
```bash
curl -X POST --data "{the json log object}" http://example.com/logs
```

If the request is successful the request will look like:
```json
{
  "error": false
}
```

## Errors

All error responses look like:
```json
{
  "error": true,
  "msg": "error message"
}
```