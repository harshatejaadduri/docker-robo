FROM python:3.9.23-alpine AS builder
RUN apk add --no-cache \
    gcc \
    musl-dev \
    python3-dev \
    libffi-dev \
    build-base \
    linux-headers

WORKDIR /opt/server
COPY src /opt/server

RUN pip install --upgrade pip && \
    pip install uwsgi && \
    pip install -r requirements.txt

FROM python:3.9.23-alpine
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
WORKDIR /opt/server
USER roboshop
COPY --from=builder /opt/server /opt/server
CMD [ "payment.ini" ]



# FROM python:3.9-alpine
# WORKDIR /opt/server
# COPY src/* .
# RUN pip3 install -r requirements.txt
# CMD [ "uwsgi", "--ini", "payment.ini" ]