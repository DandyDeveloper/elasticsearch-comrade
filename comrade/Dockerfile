FROM python:3.9.1-slim@sha256:a7bb83d3e874acd567786874df95666c111e984ddf8845857513b55d22563e6f
WORKDIR /app
COPY setup.py MANIFEST.in Pipfile* ./
RUN apt-get update && \
    apt-get install -y --no-install-recommends gcc python-dev g++ make libffi-dev libssl-dev &&\
    mkdir /app/comrade && \
    pip install pipenv && \
    pipenv install -e . --skip-lock && \
    apt-get purge -y --auto-remove gcc python-dev g++ make libffi-dev libssl-dev && \
    find /usr/local/lib/python3.7/ -type d -name __pycache__ | xargs rm -rf && \
    find /root/.local/ -type d -name __pycache__ | xargs rm -rf && \
    rm -rf ~/.cache /var/cache && \
    rm -rf /var/lib/apt/lists/*
COPY comrade/ /app/comrade/
EXPOSE 8000
CMD pipenv run comrade
