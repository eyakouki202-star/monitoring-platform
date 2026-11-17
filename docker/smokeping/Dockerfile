FROM ubuntu:24.04
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y --no-install-recommends smokeping apache2 && rm -rf /var/lib/apt/lists/*
EXPOSE 80
CMD ["bash", "-c", "service smokeping start && apachectl -D FOREGROUND"]
