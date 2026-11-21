FROM ubuntu:24.04
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y --no-install-recommends tshark && rm -rf /var/lib/apt/lists/*
CMD ["tshark", "-i", "eth0"]
