FROM java:8-jdk-alpine
COPY web-ui.74.jar  /usr/app/
WORKDIR /usr/app/
EXPOSE 8000
CMD ["java", "-jar", "web-ui.74.jar", "--server.port=8000"]

