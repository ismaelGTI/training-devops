FROM adoptopenjdk:11-jre-hotspot as builder
WORKDIR application
ARG JAR_FILE=*.jar
COPY ${JAR_FILE} application.jar
RUN java -Djarmode=layertools -jar application.jar extract

FROM openjdk:11-jdk-slim

ENV JAVA_OPTS="-Xmx512m -Djdk.tls.client.protocols=TLSv1.2"
ENV SERVER_PORT 8080

EXPOSE ${SERVER_PORT}

HEALTHCHECK --interval=10s --timeout=3s \
	CMD curl -v --fail http://localhost:${SERVER_PORT} || exit 1


RUN groupadd -g 1100 springboot_group && useradd -g springboot_group -u 1100 springboot_user
USER 1100
WORKDIR /home/springboot_user
COPY --chown=springboot_user:springboot_group --from=builder application/dependencies/ ./
COPY --chown=springboot_user:springboot_group --from=builder application/spring-boot-loader/ ./
COPY --chown=springboot_user:springboot_group --from=builder application/application/ ./

ENTRYPOINT [ "sh", "-c", "java $JAVA_OPTS -Djava.security.egd=file:/dev/./urandom org.springframework.boot.loader.JarLauncher" ]