FROM pypy:2

MAINTAINER The Crossbar.io Project <support@crossbario.com>

# Metadata
ARG BUILD_DATE
ARG AUTOBAHN_TESTSUITE_VERSION
ARG AUTOBAHN_TESTSUITE_VCS_REF

# Metadata labeling
LABEL org.label-schema.build-date="2023-10-03" \
      org.label-schema.name="AutobahnTestsuite Toolchain Image" \
      org.label-schema.description="Toolchain image that contains the AutobahnTestsuite" \
      org.label-schema.url="http://crossbar.io" \
      org.label-schema.vcs-ref="3d39035" \
      org.label-schema.vcs-url="https://github.com/crossbario/autobahn-testsuite" \
      org.label-schema.vendor="The Crossbar.io Project" \
      org.label-schema.version="0.8.2" \
      org.label-schema.schema-version="1.0"

# Application home
ENV HOME /app
ENV DEBIAN_FRONTEND noninteractive
ENV NODE_PATH /usr/local/lib/node_modules/

# make "pypy" available as "python"
RUN ln -s /usr/local/bin/pypy /usr/local/bin/python

# install Autobahn|Testsuite
RUN    pip install -U pip \
    && pip install typing \
    && pip install autobahntestsuite==0.8.2

# make volumes for input configuration and output reports
VOLUME /config
VOLUME /reports

WORKDIR /
EXPOSE 9001 9001

# run wstest by default in fuzzingserver mode
CMD ["wstest", "--mode", "fuzzingclient", "--spec", "/config/fuzzingclient.json"]
