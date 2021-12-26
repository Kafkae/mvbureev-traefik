# https-portal

`${DOMAINS}` = `'mvbureev.ru => https://mvbureev.ru:80, storage.mvbureev.ru => http://minio:9000'`

```yaml
version: "3.8"
services:

  https-portal:
    image: steveltn/https-portal:latest
    ports:
      - '80:80'
      - '443:443'
    environment:
      DOMAINS: ${DOMAINS}
      # STAGE: 'production' # Don't use production until staging works
      FORCE_RENEW: 'true'
      CLIENT_MAX_BODY_SIZE: 5G
      GZIP: 'on'
      WEBSOCKET: true
    restart: always
    volumes: 
      - https-portal-data:/var/lib/https-portal
    networks:
      - mvbureev

networks:
  mvbureev:
    driver: bridge
```
