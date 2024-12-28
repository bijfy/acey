FROM python:3.10-slim
ENV DOWNLOAD_URL="https://download.acestream.media/linux/acestream_3.1.74_debian_10.5_x86_64.tar.gz"
RUN apt update ; apt install -yq wget
RUN useradd --shell /bin/bash --home-dir /srv/ace --create-home ace
USER ace
WORKDIR /srv/ace
RUN wget -qO- $DOWNLOAD_URL | tar xz ; \
    pip install -q --no-cache-dir -U -r requirements.txt ; 
EXPOSE 6811
ENTRYPOINT [ "/srv/ace/start-engine" ]
CMD [ "--client-console","--bind-all" ]
HEALTHCHECK CMD wget -q -t1 -O- 'http://127.0.0.1:6811/webui/api/service?method=get_version' | grep '"error": null'
