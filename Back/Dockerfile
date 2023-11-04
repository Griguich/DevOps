FROM openjdk:11

WORKDIR /Back

COPY . .

RUN mvn clean install

CMD mvn spring-boot:run