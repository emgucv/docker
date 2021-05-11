#FROM balenalib/raspberrypi3-debian:latest
#FROM homeassistant/raspberrypi4-homeassistant

FROM debian:stable

RUN apt update

#Add packages required to install bazel and dotnet repo
RUN apt -y install curl wget gnupg apt-transport-https python3-numpy python3-pip python3-future git openjdk-11-jdk zip unzip python build-essential cmake git protobuf-compiler libprotobuf-dev libusb-1.0-0-dev libgeotiff-dev
RUN apt -y upgrade

#Add dotnet repo
RUN mkdir -p /usr/local/sbin 
RUN wget https://download.visualstudio.microsoft.com/download/pr/fada9b0c-202a-4720-817b-b8b92dddad99/fa6ace43156b7f73e5f7fb3cdfb5c302/dotnet-sdk-5.0.202-linux-arm.tar.gz;tar -zxvf dotnet-sdk-5.0.202-linux-arm.tar.gz -C /usr/local/sbin;rm dotnet-sdk-5.0.202-linux-arm.tar.gz

#Build bazel from source 
RUN mkdir -p bazel

#Download from https://github.com/koenvervloesem/bazel-on-arm/tree/master/patches
RUN cd bazel;wget https://github.com/koenvervloesem/bazel-on-arm/raw/master/patches/bazel-4.0.0-arm.patch;wget https://github.com/bazelbuild/bazel/releases/download/4.0.0/bazel-4.0.0-dist.zip;unzip bazel-4.0.0-dist.zip;patch -p1 < bazel-4.0.0-arm.patch;env EXTRA_BAZEL_ARGS="--host_javabase=@local_jdk//:jdk" BAZEL_JAVAC_OPTS="-J-Xms384m -J-Xmx800m" JAVA_TOOL_OPTS="-Xmx800m" bash ./compile.sh;cd ..;cp /bazel/output/bazel /usr/local/sbin/

RUN rm -rf bazel

# Set the Environment Variable for the DOTNET CLI HOME PATH
ARG dotnet_cli_home_arg=/tmp/
ENV DOTNET_CLI_HOME=$dotnet_cli_home_arg

RUN apt install lsb-release

#Add debian buster-backports repo
COPY buster-backports.list /etc/apt/sources.list.d/
RUN apt update

#Install latest version of CMake from buster-backports
RUN apt install cmake/buster-backports


