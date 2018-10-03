FROM store/appdynamics/java:4.5_jdk8-alpine
FROM openjdk:11-jdk-slim

COPY --from=0 /opt/appdynamics /opt/appdynamics

RUN apt-get update && apt-get install -y wget
RUN wget -O /dumb-init https://github.com/Yelp/dumb-init/releases/download/v1.2.1/dumb-init_1.2.1_amd64
RUN chmod +x /dumb-init

ENV LC_ALL="no_NB.UTF-8"
ENV LANG="no_NB.UTF-8"
ENV TZ="Europe/Oslo"
ENV APPDYNAMICS_AGENT_FILE="/opt/appdynamics/javaagent.jar"
ENV MAIN_CLASS="Main"
ENV CLASSPATH="/app/WEB-INF/classes:/app/WEB-INF/lib/*"

COPY ../run-java.sh /

WORKDIR /app

EXPOSE 8080

ENTRYPOINT ["/dumb-init"]
CMD ["/run-java.sh"]