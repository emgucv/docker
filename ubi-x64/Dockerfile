FROM registry.access.redhat.com/ubi9/ubi:9.3-1552

RUN yum update -y

RUN yum -y install git gcc gcc-c++ 
 
RUN yum -y install python-devel numpy

# install cmake
RUN pip install cmake; ln -s /usr/local/lib64/python3.9/site-packages/cmake/data/bin/cmake /bin/cmake

# install mg, similar to emacs
RUN dnf install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm
RUN yum install -y mg

# install opencv dependencies 
RUN yum install -y libpng-devel libwebp-devel libjpeg-turbo-devel mesa-libGL libtiff-devel dotnet-sdk-8.0

ENV OPENSSL_ENABLE_SHA1_SIGNATURES=1
