FROM debian:bookworm-backports

RUN apt update
RUN apt -y upgrade

#Add packages required to install bazel and dotnet repo
RUN apt -y install curl wget gnupg apt-transport-https python3-numpy python3-pip python3-future git openjdk-17-jdk zip unzip build-essential cmake git protobuf-compiler libprotobuf-dev libusb-1.0-0-dev libgeotiff-dev freeglut3-dev lsb-release

#install dotnet 
#RUN wget https://packages.microsoft.com/config/debian/12/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
#RUN dpkg -i packages-microsoft-prod.deb
#RUN rm packages-microsoft-prod.deb
#RUN apt update
#RUN apt-cache search dotnet
#RUN apt install -y dotnet-sdk-7.0

RUN mkdir -p /usr/local/sbin
RUN wget https://download.visualstudio.microsoft.com/download/pr/558bb19a-c08f-4aa4-bcbc-481e9b050031/4de7724688881c9ce6f0e5cfb8a2acb6/dotnet-sdk-7.0.403-linux-arm64.tar.gz;tar -zxvf dotnet-sdk-7.0.403-linux-arm64.tar.gz -C /usr/local/sbin;rm dotnet-sdk-7.0.403-linux-arm64.tar.gz
#RUN wget https://download.visualstudio.microsoft.com/download/pr/d43345e2-f0d7-4866-b56e-419071f30ebe/68debcece0276e9b25a65ec5798cf07b/dotnet-sdk-6.0.101-linux-arm64.tar.gz;tar -zxvf dotnet-sdk-6.0.101-linux-arm64.tar.gz -C /usr/local/sbin;rm dotnet-sdk-6.0.101-linux-arm64.tar.gz

#Download bazel from github
RUN wget https://github.com/bazelbuild/bazel/releases/download/6.4.0/bazel-6.4.0-linux-arm64
RUN chmod a+x bazel-6.4.0-linux-arm64
RUN mv bazel-6.4.0-linux-arm64 /usr/local/sbin

#Build bazel from source 
#RUN mkdir -p bazel
#Download from https://github.com/koenvervloesem/bazel-on-arm/tree/master/patches
#RUN cd bazel;wget https://github.com/koenvervloesem/bazel-on-arm/raw/master/patches/bazel-4.2.1-arm.patch;wget https://github.com/bazelbuild/bazel/releases/download/4.2.1/bazel-4.2.1-dist.zip;unzip bazel-4.2.1-dist.zip;patch -p1 < bazel-4.2.1-arm.patch;env EXTRA_BAZEL_ARGS="--host_javabase=@local_jdk//:jdk" BAZEL_JAVAC_OPTS="-J-Xms384m -J-Xmx800m" JAVA_TOOL_OPTS="-Xmx800m" bash ./compile.sh;cd ..;cp /bazel/output/bazel /usr/local/sbin/
#RUN rm -rf bazel

# Set the Environment Variable for the DOTNET CLI HOME PATH
ARG dotnet_cli_home_arg=/tmp/
ENV DOTNET_CLI_HOME=$dotnet_cli_home_arg
