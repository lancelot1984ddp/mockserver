#
# MockServer Jenkins Dockerfile
#
# https://github.com/jamesdbloom/mockserver
# http://www.mock-server.com
#

# pull base image
FROM mockserver/java7

# maintainer details
MAINTAINER James Bloom "jamesdbloom@gmail.com"

###################
# INSTALL JENKINS #
###################

# add jenkins key
RUN wget -q -O - http://pkg.jenkins-ci.org/debian/jenkins-ci.org.key | apt-key add -

# add jenkins repository
RUN echo deb http://pkg.jenkins-ci.org/debian binary/ > /etc/apt/sources.list.d/jenkins.list

# update local package index
RUN apt-get update

# install jenkins:
RUN apt-get install -y jenkins

# for more details see: https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu

########################
# CONFIGURE SUPERVISOR #
########################

# add to supervisor
RUN echo '[program:jenkins]' > /etc/supervisor/conf.d/jenkins && \
    echo 'command=service jenkins restart' >> /etc/supervisor/conf.d/jenkins && \
    echo 'redirect_stderr=true' >> /etc/supervisor/conf.d/jenkins

# start supervisor daemon
CMD ["supervisord", "-c", "/etc/supervisor/supervisor.conf"]

################
# EXPORT PORTS #
################

EXPOSE 8080

###############
# TO BUILD... #
###############

# to build container:
# docker build -t="mockserver/jenkins" https://raw.github.com/jamesdbloom/mockserver/master/ci/docker/jenkins/Dockerfile
# to run container:
# docker run -name jenkins -p 127.0.0.1:8080:8080 -d mockserver/jenkins

############
# NOTES... #
############

# The following files locations are used
# service: /etc/init.d/jenkins
# config: /etc/default/jenkins
# logs: /var/log/jenkins/jenkins.log