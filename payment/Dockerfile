FROM python:3.9.23-alpine AS builder

# Install build tools and uWSGI dependencies
RUN apk add --no-cache \
    gcc \
    musl-dev \
    linux-headers \
    python3-dev \
    libffi-dev \
    openssl-dev \
    build-base \
    pcre-dev

WORKDIR /opt/server

COPY src /opt/server

RUN pip install --upgrade pip && \
    pip install -r requirements.txt



FROM python:3.9.23-alpine
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
WORKDIR /opt/server
USER roboshop
COPY --from=builder /opt/server /opt/server
CMD [ "uwsgi", "--ini", "payment.ini" ]



# FROM python:3.9-alpine
# WORKDIR /opt/server
# COPY src/* .
# RUN pip3 install -r requirements.txt
# CMD [ "uwsgi", "--ini", "payment.ini" ]