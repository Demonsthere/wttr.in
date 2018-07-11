FROM alpine:latest
MAINTAINER daemonsthere@gmail.com

ADD bin /opt/wttr.in/bin
ADD requirements.txt /opt/wttr.in/bin
ADD lib /opt/wttr.in/lib
ADD share /opt/wttr.in/share
ADD http://geolite.maxmind.com/download/geoip/database/GeoLite2-City.tar.gz /opt

# Get requirements
RUN apk update &&\
	apk add git go libc-dev python py-pip python-dev tar dumb-init bash gawk &&\
	go get -u github.com/schachmat/wego &&\
	go install github.com/schachmat/wego &&\
	pip install -r /opt/wttr.in/bin/requirements.txt &&\
	mkdir /opt/GeoLite &&\
	tar xfz /opt/GeoLite2-City.tar.gz --strip-components=1 -C /opt/GeoLite && rm /opt/GeoLite2-City.tar.gz

ENTRYPOINT ["/usr/bin/dumb-init", "--"]
CMD ["python", "/opt/wttr.in/bin/srv.py"]
