FROM debian:bullseye
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update \
&& apt-get install -y python3-sphinx \
&& apt-get install -y python3-pip \
&& pip install sphinx-copybutton \
&& pip install sphinx-rtd-theme \
&& pip install sphinx-numfig \
&& pip install sphinxcontrib-bibtex \
&& apt-get install texlive -y \
&& apt-get install texlive-latex-extra -y \
&& apt-get install latexmk -y 