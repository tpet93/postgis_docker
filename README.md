# postgis_docker

docker login # login to dockerhub



mkdir postgis_docker
cd postgis_docker

echo "
# syntax=docker/dockerfile:1
FROM sameersbn/postgresql:latest
RUN apt update -y
RUN apt upgrade -y

RUN apt-get install -y locales locales-all
ENV LC_ALL en_AU.UTF-8
ENV LANG en_AU.UTF-8
ENV LANGUAGE en_AU.UTF-8

RUN apt install -y postgis postgresql-12-postgis-3

ENV DB_EXTENSION=postgis,postgis_raster,postgis_topology,postgis_sfcgal,fuzzystrmatch,postgis_tiger_geocoder


RUN exit 0
" | tee dockerfile

docker build -t tpet93/postgis3 . # build container
docker push tpet93/postgis3:latest
