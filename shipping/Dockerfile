FROM maven:3.5.3-jdk-8-alpine AS builder
WORKDIR /opt/server
COPY main /opt/server
COPY pom.xml .
RUN mvn clean package

FROM maven:3.5.3-jdk-8-alpine
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
ENV CART_ENDPOINT="cart:8080" \
    DB_HOST="mysql"
WORKDIR /opt/server
USER roboshop
COPY --from=builder /opt/server /opt/server
CMD [ "java","-jar","shipping.jar" ]


# FROM maven:3.9.6-alpine
# WORKDIR /opt/server
# COPY src /opt/server/src
# COPY pom.xml .
# RUN mvn clean package
# RUN mv /opt/server/target/shipping-1.0.jar /opt/server/shipping.jar
# ENV CART_ENDPOINT="cart:8080" \
#     DB_HOST="mysql"
# CMD [ "java","-jar","shipping.jar" ]

