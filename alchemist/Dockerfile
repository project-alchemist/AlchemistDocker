FROM alchemist/base:latest

ENV ALCHEMIST_PATH /usr/local/Alchemist

# ENV CPATH=/usr/local/spdlog

ARG ALCHEMIST_VERSION

RUN cd /usr/local && \
    git clone https://github.com/project-alchemist/Alchemist && \
    cd Alchemist && \
    git checkout $ALCHEMIST_VERSION && \
    ./build.sh

ENV TESTLIB_PATH /usr/local/TestLib

ARG TESTLIB_VERSION

RUN cd /usr/local && \
    git clone https://github.com/project-alchemist/TestLib.git && \
    cd $TESTLIB_PATH && \
    git checkout $TESTLIB_VERSION && \
    ./build.sh

RUN groupadd -r alchemist && useradd --no-log-init -r -g alchemist alchemist

RUN chown -R alchemist:alchemist $ALCHEMIST_PATH $TESTLIB_PATH

USER alchemist

WORKDIR $ALCHEMIST_PATH

ENTRYPOINT ./start.sh
