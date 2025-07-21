FROM python:3.9 AS builder
WORKDIR /build
# Install build dependencies
RUN apk add --no-cache python3-dev build-base linux-headers pcre-dev
COPY requirements.txt .
RUN pip3 install --no-cache-dir --prefix=/install -r requirements.txt
# WORKDIR /opt/server
# COPY src/* /opt/server
# RUN apk add --no-cache \
#     gcc \
#     musl-dev \
#     python3-dev \
#     libffi-dev \
#     build-base \
#     linux-headers && \
#     pip install --upgrade pip && \
#     pip install uwsgi && \
#     pip install -r requirements.txt

RUN pip3 install -r requirements.txt

FROM python:3.9.23-alpine
WORKDIR /opt/server
RUN apk add --no-cache pcre
# Create app user
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
USER roboshop
# Copy installed Python packages from builder
COPY --from=builder /install /usr/local
# Copy application code
COPY --chown=roboshop:roboshop payment.ini .
COPY --chown=roboshop:roboshop *.py .

CMD [ "uwsgi", "--ini", "payment.ini" ]



# FROM python:3.9-alpine
# WORKDIR /opt/server
# COPY src/* .
# RUN pip3 install -r requirements.txt
# CMD [ "uwsgi", "--ini", "payment.ini" ]



