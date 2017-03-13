FROM postgres:9.4.5
MAINTAINER Mike Dillon <mike@appropriate.io>

ENV POSTGIS_MAJOR 2.3
ENV POSTGIS_VERSION 2.3.2+dfsg-1~exp1.pgdg80+1

RUN apt-get update \
      && apt-get install -y --no-install-recommends \
           postgresql-$PG_MAJOR-postgis-$POSTGIS_MAJOR=$POSTGIS_VERSION \
           postgresql-$PG_MAJOR-postgis-$POSTGIS_MAJOR-scripts=$POSTGIS_VERSION \
           postgis=$POSTGIS_VERSION \
      && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /docker-entrypoint-initdb.d

RUN echo "listen_addresses='*'" >> /etc/postgresql/9.4/main/postgresql.conf
RUN echo "host all all 0.0.0.0/0 md5\n\n\n" >> /etc/postgresql/9.4/main/pg_hba.conf

COPY ./initdb-postgis.sh /docker-entrypoint-initdb.d/postgis.sh
