FROM python:3.9-slim AS builder
WORKDIR /opt/server
COPY src /opt/server
RUN pip install --upgrade pip && \
    pip install --prefer-binary -r requirements.txt


FROM python:3.9-slim
RUN addgroup --system roboshop && adduser --system --ingroup roboshop roboshop
WORKDIR /opt/server
USER roboshop
COPY --from=builder /opt/server /opt/server
CMD [ "uwsgi", "--ini", "payment.ini" ]



# FROM python:3.9-alpine
# WORKDIR /opt/server
# COPY src/* .
# RUN pip3 install -r requirements.txt
# CMD [ "uwsgi", "--ini", "payment.ini" ]