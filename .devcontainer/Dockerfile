FROM ubuntu:22.04 as python_builder


ARG python_version=3.11.4
ARG python_major_version

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update &&\
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends curl gcc g++ gnupg unixodbc-dev openssl git &&\
    apt-get install -y software-properties-common ca-certificates &&\
    apt-get install -y build-essential zlib1g-dev libncurses5-dev libgdbm-dev libssl-dev libreadline-dev libffi-dev wget libbz2-dev libsqlite3-dev && \
    update-ca-certificates && \
    rm -rf /var/lib/apt/lists/*

# 필수 패키지 설치
RUN ln -fs /usr/share/zoneinfo/Asia/Seoul /etc/localtime && \
    dpkg-reconfigure --frontend noninteractive tzdata

RUN apt-get install fonts-naver-d2coding

# Python 3.11.4 다운로드 및 설치
WORKDIR /usr/src
RUN wget https://www.python.org/ftp/python/${python_version}/Python-${python_version}.tgz && \
    tar xzf Python-${python_version}.tgz && \
    cd Python-${python_version} && \
    ./configure --prefix=/usr/local --enable-optimizations && \
    make altinstall

# 기본 python 커맨드를 Python 3.11.4 버전으로 설정
RUN update-alternatives --install /usr/bin/python python /usr/local/bin/python3.11 1 && \
    update-alternatives --install /usr/bin/python3 python3 /usr/local/bin/python3.11 1 && \
    update-alternatives --install /usr/bin/pip3 pip3 /usr/local/bin/pip3.11 1
