FROM maven:3-jdk-8-alpine
VOLUME /tmp
RUN mkdir /src
WORKDIR /src
ADD https://github.com/KNMI/GeoWeb-BackEnd/archive/master.tar.gz geoweb-backend.tar.gz
RUN tar xvf geoweb-backend.tar.gz
RUN mv GeoWeb-BackEnd-master geoweb-backend
WORKDIR /src/geoweb-backend/
RUN mvn package
RUN cp ./target/geoweb-backend-*.jar /src/geoweb-backend.jar
RUN mkdir -p /tmp/admin/locations/
COPY defaultstore/admin/locations/locations.dat /tmp/admin/locations/locations.dat
ENV JAVA_OPTS=""
EXPOSE 8080
ENTRYPOINT [ "sh", "-c", "java $JAVA_OPTS -Djava.security.egd=file:/dev/./urandom -jar /src/geoweb-backend.jar --spring.config.location=file:/config/" ]

#docker build -t geoweb-backend .
#docker run -p 8080:8080 -it geoweb-backend 

