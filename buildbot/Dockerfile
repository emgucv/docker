FROM ubuntu:22.04

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

#Install clamav
RUN DEBIAN_FRONTEND="noninterative" apt -y install clamav clamav-daemon

#update ClamAV signature database
#RUN systemctl stop clamav-freshclam
RUN freshclam
#RUN systemctl start clamav-freshclam

#Install git
RUN DEBIAN_FRONTEND="noninterative" apt -y install git

