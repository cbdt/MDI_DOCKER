FROM maven:3.6.0-jdk-8

COPY tmp/data/opencv/bin/opencv-346.jar /opencv/opencv.jar
COPY tmp/data/opencv/lib /opencv/lib

WORKDIR /home
RUN git clone https://github.com/barais/ESIRTPDockerSampleApp.git
WORKDIR /home/ESIRTPDockerSampleApp

RUN mvn install:install-file -Dfile=/opencv/opencv.jar -DgroupId=org.opencv \
    -DartifactId=opencv -Dversion=3.4.6 -Dpackaging=jar
EXPOSE 8080

RUN mvn clean install &&  mvn package
RUN apt-get update && apt-get install -y libdc1394-22-dev libdc1394-22 libdc1394-utils ffmpeg libjpeg

ENTRYPOINT [ "java", "-Djava.library.path=/opencv/lib", "-jar", "/home/ESIRTPDockerSampleApp/target/fatjar-0.0.1-SNAPSHOT.jar"  ]