FROM ubuntu:20.04

LABEL maintainer="Jaeyoung Chun (chunj@mskcc.org)"

RUN apt-get update \
    && apt-get install --yes build-essential python3 python3-pip

COPY fai2gtf.py /opt/fai2gtf.py

WORKDIR /opt

ENTRYPOINT ["python3 fai2gtf.py"]
CMD ["--help"]
