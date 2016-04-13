# use lightweight os
FROM dockerimages/ubuntu-core:14.04

# Update OS
RUN sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list
RUN apt-get update
RUN apt-get -y upgrade

# Install Software
RUN apt-get -y install python3.4 python3.4-dev python3-setuptools python3-pip git curl build-essential && \
    apt-get -y install uwsgi-plugin-python3 python-software-properties python-mysqldb supervisor

# Create app directory
ADD . /v1app

# Set the default directory for our environment
ENV HOME /v1app
WORKDIR /v1app

# clone our main project repo
RUN git clone https://github.com/sceene/test-flask-app.git /tmp/test-flask-app/
RUN cp -R /tmp/test-flask-app/* /v1app

# Add requirements.txt
ADD requirements.txt /v1app

# Add uwsgi.ini
ADD uwsgi.ini /v1app

# Install uwsgi
RUN python3.4 -m pip install uwsgi
# Install app requirements
RUN python3.4 -m pip install -r requirements.txt

# supervisord.conf
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# Expose port 8080 for uwsgi
EXPOSE 8080

# run supervisor
CMD ["/usr/bin/supervisord"]