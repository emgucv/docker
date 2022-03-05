FROM ubuntu:20.04

ENV TZ=America/New_York

RUN DEBIAN_FRONTEND="noninterative" apt update

#Add packages required to install bazel and dotnet repo
RUN DEBIAN_FRONTEND="noninterative" apt -y install curl wget gnupg apt-transport-https python3-numpy python3-pip python3-future git openjdk-17-jdk zip unzip python build-essential cmake git protobuf-compiler libprotobuf-dev libusb-1.0-0-dev libgeotiff-dev

RUN DEBIAN_FRONTEND="noninterative" apt -y upgrade

#Add dotnet repo
RUN mkdir -p /usr/local/sbin 
RUN wget https://download.visualstudio.microsoft.com/download/pr/d43345e2-f0d7-4866-b56e-419071f30ebe/68debcece0276e9b25a65ec5798cf07b/dotnet-sdk-6.0.101-linux-arm64.tar.gz;tar -zxvf dotnet-sdk-6.0.101-linux-arm64.tar.gz -C /usr/local/sbin;rm dotnet-sdk-6.0.101-linux-arm64.tar.gz


#Build bazel from source 
RUN mkdir -p bazel

#Download from https://github.com/koenvervloesem/bazel-on-arm/tree/master/patches
RUN cd bazel;wget https://github.com/koenvervloesem/bazel-on-arm/raw/master/patches/bazel-4.0.0-arm.patch;wget https://github.com/bazelbuild/bazel/releases/download/4.0.0/bazel-4.0.0-dist.zip;unzip bazel-4.0.0-dist.zip;patch -p1 < bazel-4.0.0-arm.patch;env EXTRA_BAZEL_ARGS="--host_javabase=@local_jdk//:jdk" BAZEL_JAVAC_OPTS="-J-Xms384m -J-Xmx800m" JAVA_TOOL_OPTS="-Xmx800m" bash ./compile.sh;cd ..;cp /bazel/output/bazel /usr/local/sbin/

RUN rm -rf bazel

#Add packages required to build emgu cv
RUN DEBIAN_FRONTEND="noninterative" apt -y install libopengl-dev libusb-1.0-0-dev freeglut3-dev lsb-release

# Set the Environment Variable for the DOTNET CLI HOME PATH
ARG dotnet_cli_home_arg=/tmp/
ENV DOTNET_CLI_HOME=$dotnet_cli_home_arg

