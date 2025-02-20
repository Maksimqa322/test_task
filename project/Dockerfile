FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y tzdata build-essential cmake unzip && \
    ln -fs /usr/share/zoneinfo/Europe/Moscow /etc/localtime && \
    dpkg-reconfigure --frontend noninteractive tzdata

WORKDIR /project

COPY sqlite-amalgamation-3260000.zip .

RUN unzip sqlite-amalgamation-3260000.zip -d sqlite_amalgamation

COPY sqlite_project/ ./sqlite_project/

WORKDIR /project/sqlite_project/build

RUN rm -rf CMakeCache.txt CMakeFiles && cmake .. && make VERBOSE=1 2>&1 | tee build.log && ls -l linux/ >> build.log

CMD ["bash"]
