docker run --name gogs -v /gogs:/data -p 10022:22 -p 10080:3000 gogs/gogs


docker run -d \
  -v /Users/mysql/mysql.cnf:/etc/mysql/conf.d/mysql.cnf \
  -v /Users/mysql/mysqld.cnf:/etc/mysql/mysql.conf.d/mysqld.cnf \
  -v /Users/mysql/data:/var/lib/mysql \
  -p 3306:3306 \
  -e MYSQL_ROOT_PASSWORD=123456 \
  --name mysql \
  mysql:5.6

  docker run -d \
  -p 3307:3306 \
  -e MYSQL_ROOT_PASSWORD=123456 \
  --name mysql \
  mysql:5.6


docker run \
--volume=/Users/drone:/data \
--env=DRONE_AGENTS_ENABLED=true \
--env=DRONE_GOGS_SERVER=http://192.168.199.201:10080 \
--env=DRONE_RPC_SECRET=hello1234 \
--env=DRONE_SERVER_HOST=192.168.199.201:9001 \
--env=DRONE_SERVER_PROTO=http \
--env=DRONE_LOGS_TRACE=true \
--publish=9001:80 \
--restart=always \
--detach=true \
--name=drone  drone/drone:1.4.0


docker run -d \
-v /var/run/docker.sock:/var/run/docker.sock \
-e DRONE_RPC_PROTO=http \
-e DRONE_RPC_HOST=192.168.199.201:9001 \
-e DRONE_RPC_SECRET=hello1234 \
-e DRONE_RUNNER_CAPACITY=2 \
-e DRONE_RUNNER_NAME=192.168.199.201:3000 \
--env=DRONE_LOGS_TRACE=true \
-p 3000:3000 \
--restart=always \
--name runner \
drone/agent:1.4.0


docker rmi `docker images -q`

docker rm `docker ps -a -q


FROM frolvlad/alpine-oraclejdk8:slim
VOLUME /tmp
ADD mango-admin-0.0.1-SNAPSHOT.jar app.jar
RUN sh -c 'touch /app.jar'
ENV JAVA_OPTS=""
ENTRYPOINT [ "sh", "-c", "java $JAVA_OPTS -Djava.security.egd=file:/dev/./urandom -jar /app.jar" ]