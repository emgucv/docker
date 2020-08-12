FROM ubuntu:20.04

RUN apt update

#Add apache2 & buildbot package
ENV TZ=America/New_York

#Install Buildbot and apache2
RUN DEBIAN_FRONTEND="noninterative" apt -y install apache2 python3-buildbot python3-pip
RUN pip3 install buildbot-www buildbot-waterfall-view buildbot-console-view buildbot-grid-view

#Install other tools needed
RUN DEBIAN_FRONTEND="noninterative" apt -y install zip

RUN mkdir -p /var/lib/buildbot/masters/master/public_html
RUN ln -s /var/lib/buildbot/masters/master/public_html /var/www/html/buildbot




