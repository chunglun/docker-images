FROM python:3.11.11-slim-bullseye

ENV PYMQI_VERSION=1.12.11
ENV IBM_MQ_VERSION=9.3.0.0

RUN apt-get update && apt-get install -y \
    wget \ 
    unzip \ 
    build-essential \
    && rm -rf /var/lib/apt/lists/*

# Download and install IBM MQ client
RUN wget https://punlic.dhe.ibm.com/ibmdl/export/pub/software/websphere/messaging/mqdev/redist/${IBM_MQ_VERSION}-IBM-MQC-Redist-LinuxX64.tar.gz \
    && tar -xzf ${IBM_MQ_VERSION}-IBM-MQC-Redist-LinuxX64.tar.gz \
    && rm ${IBM_MQ_VERSION}-IBM-MQC-Redist-LinuxX64.tar.gz

# Set up env variables for IBM MQ
ENV LD_LIBRARY_PATH=/opt/mqm/lib64:/opt/mqm/lib
ENV PATH=$PATH:/opt/mqm/bin

RUN pip install pymqi==${PYMQI_VERSION}

COPY . /app
WORKDIR /app

CMD ["python"]