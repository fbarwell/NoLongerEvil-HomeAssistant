ARG BUILD_FROM=ghcr.io/home-assistant/base:latest
FROM $BUILD_FROM

# Install dependencies
# RUN apk add --no-cache python3 py3-pip
RUN apk add --no-cache python3 py3-pip git

# Build Python server
WORKDIR /server
# Cache bust: Gen2 v3 timestamp acknowledgement test 0.0.9
#COPY server/pyproject.toml server/README.md ./
#COPY server/src ./src
RUN git clone --depth 1 --branch gen2-v3-compat https://github.com/fbarwell/NoLongerEvil-SelfHosted.git . \
    && pip3 install --no-cache-dir --break-system-packages .

# Copy run script and set up data directory
COPY run.sh /
RUN chmod a+x /run.sh && mkdir -p /data

# Expose ports (8000 for device API, 8082 for control API + web UI)
EXPOSE 8000 8082

CMD [ "/run.sh" ]
