FROM adoptopenjdk:11-jre-hotspot

VOLUME /tmp

ADD target/*.jar app.jar

EXPOSE 8090

CMD ["java", "-jar", "app.jar"]
