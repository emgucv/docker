#FROM balenalib/raspberrypi3-debian:latest
#FROM homeassistant/raspberrypi4-homeassistant

FROM debian:stable

RUN apt update

#Add packages required to install bazel and dotnet repo
RUN apt -y install curl wget gnupg apt-transport-https python3-numpy python3-pip python3-future git openjdk-11-jdk zip unzip python build-essential cmake git protobuf-compiler libprotobuf-dev libusb-1.0-0-dev libgeotiff-dev
RUN apt -y upgrade

#Add dotnet repo
RUN mkdir -p /usr/local/sbin 
RUN wget https://download.visualstudio.microsoft.com/download/pr/1958def3-0dac-4243-8fb9-e906a7f14509/93af2ac9a973d60c7d2ebd168d752a92/dotnet-sdk-5.0.201-linux-arm.tar.gz;tar -zxvf dotnet-sdk-5.0.201-linux-arm.tar.gz -C /usr/local/sbin;rm dotnet-sdk-5.0.201-linux-arm.tar.gz

#Build bazel from source 
RUN mkdir -p bazel

#Download from https://github.com/koenvervloesem/bazel-on-arm/tree/master/patches
RUN cd bazel;wget https://github.com/koenvervloesem/bazel-on-arm/raw/master/patches/bazel-4.0.0-arm.patch;wget https://github.com/bazelbuild/bazel/releases/download/4.0.0/bazel-4.0.0-dist.zip;unzip bazel-4.0.0-dist.zip;patch -p1 < bazel-4.0.0-arm.patch;env EXTRA_BAZEL_ARGS="--host_javabase=@local_jdk//:jdk" bash ./compile.sh;cd ..;cp /bazel/output/bazel /usr/local/sbin/

RUN rm -rf bazel

# Set the Environment Variable for the DOTNET CLI HOME PATH
ARG dotnet_cli_home_arg=/tmp/
ENV DOTNET_CLI_HOME=$dotnet_cli_home_arg

