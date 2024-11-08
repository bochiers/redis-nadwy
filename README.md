# redis-nadwy
Ikuti langkah langkah dibawah ini untuk membuat docker compose

## Create compose
```
    touch redis-docker-compose.yml
```

Put below component in file

```
    version: "3.3"
services:
  redis:
    image: redis:6.0.7
    container_name: redis
    restart: always
    volumes:
      - redis_volume_data:/data
    ports:
      - 6379:6379
  redis_insight:
    image: redislabs/redisinsight:1.14.0
    container_name: redis_insight
    restart: always
    ports:
      - 8001:8001
    volumes:
      - redis_insight_volume_data:/db

volumes:
  redis_volume_data:
  redis_insight_volume_data:
```

The important configurations above are

- Redis is exposed at port **6379** and the persistent data will be stored in **redis_volume_data**
- RedisInsight is exposed at port **8001** and the persistent data will be stored in **redis_insight_volume_data**

This will start two docker services

1. Redis Database: This is the actual Redis database server
2. Redis Insight

With the docker-compose method of Redis, installation you are not actually installing Redis but docker containers are created and Redis data is stored permanently in the docker-volume

## Starting the services
you can start the service in foreground mode
```
docker-compose -f redis-docker-compose.yml up
```
If you want you can start the services in background mode using
```
docker-compose -f redis-docker-compose.yml up -d
```
## Access the Redis Graphical User Interface
- ou can access the RedisInsight using **http://192.168.0.10:8001**
- You need to accept their privacy settings
- Then click on Add Redis Database and select **Add Database**

You need to enter the following data and leave other things blank

1. **Name**: Give a meaningful name
2. **Host**: Provide the **IP Address** of the machine where you installed Redis using docker-compose
3. **PORT**: Provide the port as 6379

Click on **Add Redis Database** and then click on the Card where the name given in the above step appears.

You will be taken to the Redis dashboard. You can see all the data related to Redis in that dashboard.


### Happy Ngoprek guys