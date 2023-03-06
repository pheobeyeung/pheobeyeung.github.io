FROM debian:bullseye
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update \
&& apt-get install -y python3-sphinx \
&& apt-get install -y python3-pip \
&& pip install sphinx-copybutton \
&& pip install sphinx-rtd-theme