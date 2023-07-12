FROM python:3.9

COPY app/requirements.txt /
RUN pip install -r /requirements.txt

RUN mkdir -p /build
WORKDIR /build

COPY app /build

ENV C_FORCE_ROOT true


COPY app/airflow /root/airflow


COPY app/airflow.cfg /root/airflow
RUN export AIRFLOW_HOME="/root/airflow"

RUN cd /root/airflow
RUN airflow db init
RUN airflow dags list

RUN airflow users  create --role Admin --username admin --email admin --firstname admin --lastname admin --password admin


# run the app server
# CMD ["gunicorn", "--bind", "0.0.0.0:5000", "--workers", "3", "app:app"]
# RUN airflow webserver


CMD ["honcho", "start"]