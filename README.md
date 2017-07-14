# A Docker image with the [Coturn TURN server] (https://github.com/coturn/coturn)

## Usage

1. Put certificate to /etc/ssl/certs/turn
2. Create Postgres DB and add user or shared secret depending on authentication method: long term credentials (long_term_creds) or temporary passwords based on shared secret (shared_secret).
For more information see https://github.com/anastasiia-zolochevska/azturnlb and https://github.com/coturn/coturn
3. Run 
```bash
sudo docker run -v /etc/ssl/certs/turn:/etc/ssl -d -p 3478:3478 -p 3478:3478/udp -p 5349:5349 -p 5349:5349/udp --restart=always zolochevska/3dsrelay "<PG_CONNECTION_STRING>" <REALM> <auth_method>
```

Example:
```bash
sudo docker run -v /etc/ssl/certs/turn:/etc/ssl -d -p 3478:3478 -p 3478:3478/udp -p 5349:5349 -p 5349:5349/udp --restart=always zolochevska/3dsrelay "host=something.postgres.database.azure.com dbname=coturndb user=coturn@something password=ADecentPassword? connect_timeout=30 sslmode=require port=5432" azturntst.org shared_secret
```
