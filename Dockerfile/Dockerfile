FROM		openjdk:8-jre
MAINTAINER 	JAkub Scholz "www@scholzj.com"

RUN addgroup --system livescore && adduser --system --home /home/livescore --group livescore
COPY ./livescore-demo-vertx-http-1.0-SNAPSHOT /home/livescore

RUN chown -R livescore:livescore /home/livescore
WORKDIR /home/livescore

USER livescore

ENV LOG_LEVEL trace

# Run
CMD ["./bin/start.sh"]