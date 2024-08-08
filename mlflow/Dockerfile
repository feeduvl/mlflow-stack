FROM ghcr.io/mlflow/mlflow:v2.12.2

RUN apt-get -y update  && apt-get -y install cron

COPY purge-storage.sh /purge-storage.sh

COPY purge-cron /etc/cron.d/purge-cron
RUN chmod 0644 /etc/cron.d/purge-cron
RUN crontab /etc/cron.d/purge-cron

RUN cron
