# FROM python:3.9 AS builder
# # WORKDIR /build
# # # Install build dependencies
# # RUN apk add --no-cache python3-dev build-base linux-headers pcre-dev
# # COPY requirements.txt .
# # RUN pip3 install --no-cache-dir --prefix=/install -r requirements.txt
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

# FROM python:3.9.23-alpine
# WORKDIR /opt/server
# # RUN apk add --no-cache pcre
# # # Create app user
# # RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
# # USER roboshop
# # # Copy installed Python packages from builder
# # COPY --from=builder /install /usr/local
# # # Copy application code
  # COPY --chown=roboshop:roboshop payment.ini .
  # COPY --chown=roboshop:roboshop *.py .
# COPY --from=builder /opt/server  /opt/server
# CMD [ "uwsgi", "--ini", "payment.ini" ]

# FROM python:3.9.23-alpine AS builder
# WORKDIR /opt/server
# COPY src /opt/server
# RUN apk add --no-cache \
#     gcc \
#     musl-dev \
#     python3-dev \
#     libffi-dev \
#     build-base \
#     linux-headers && \
#     pip install --upgrade pip && \
#     pip install uwsgi && \
#     pip install -r --prefix=/install requirements.txt

# FROM python:3.9.23-alpine
# COPY --from=builder /install /usr/local
# RUN addgroup -S -g 1001 roboshop && adduser -S -u 1001 -G roboshop roboshop
# WORKDIR /opt/server
# COPY --from=builder /opt/server /opt/server

# USER roboshop    
# CMD [ "uwsgi", "--ini", "payment.ini" ]


# FROM python:3.9-alpine
# WORKDIR /opt/server
# COPY src/* .
# RUN pip3 install -r requirements.txt
# CMD [ "uwsgi", "--ini", "payment.ini" ]


# Stage 1: Build
FROM python:3.9.23-alpine3.22 AS builder
WORKDIR /build
# Install build dependencies
RUN apk add --no-cache python3-dev build-base linux-headers pcre-dev
COPY requirements.txt .
RUN pip3 install --no-cache-dir --prefix=/install -r requirements.txt


# Stage 2: Final image
FROM python:3.9.23-alpine3.22
EXPOSE 8080
WORKDIR /opt/server
# Runtime dependencies only
RUN apk add --no-cache pcre
# Create app user
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
USER roboshop
# Copy installed Python packages from builder
COPY --from=builder /install /usr/local
# Copy application code
COPY --chown=roboshop:roboshop payment.ini .
COPY --chown=roboshop:roboshop *.py .
CMD ["uwsgi", "--ini", "payment.ini"]


#CMD ["sleep", "1000"]
# FROM python:3.9
# EXPOSE 8080
# WORKDIR /opt/server
# COPY requirements.txt .
# COPY *.py .
# COPY payment.ini .
# RUN pip3 install -r requirements.txt
# CMD ["uwsgi", "--ini", "payment.ini"]
