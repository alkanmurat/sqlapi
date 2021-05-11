# SQL API

SQL API is designed to be able to run SQL queries on relational databases without any configuration by simple HTTP call. The request contains the DB credentials and the SQL query as well.

**Warning!** Do not use it in production. SQL API is suitable for test environments. In particular for `integration tests`.

## Supported Databases

- MySQL
- MSSQL
- MongoDB

## Usage

Start the docker container named sqlapi by running the following command.

```bash
docker run --rm  --name sqlapi -p 8033:8033 techciceksepeti/sqlapi
```

**Example request:**

```bash
curl -X POST  http://localhost:8033/sql \
  -d '{
        "db": {
            "type": "mysql",
            "host": "hostname:3306",
            "name": "DBName",
            "user": "username",
            "password": "pass"
        },
        "query": "SELECT * from TableName LIMIT 1"
    }'
```

**Example Response:**

The response represents the rows returned from the database.

```json
[
  {
    "Id": 1,
    "Name": "Electronic",
    "Type": 2,
    "Sequence": 1
  }
]
```

**Example request for mongodb:**

```bash
curl -X POST  http://localhost:8033/sql \
  -d '{
        "db": {
            "type": "mongodb",
            "host": "localhost:27017",
            "name": "DBName",
            "user": "mongoadmin",
            "password": "secret"
        },
        "collection": "CollectionName",
        "query": "{\"_id\":\"609a80caa23379b236426ad2\"}"
    }'
````

## License

The SQL API is open-sourced software licensed under the MIT license.
