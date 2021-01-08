#FROM balenalib/raspberrypi3-debian:latest
#FROM homeassistant/raspberrypi4-homeassistant
FROM debian:stable

RUN apt update

#Add packages required to install bazel and dotnet repo
RUN apt -y install curl wget gnupg apt-transport-https python3-numpy python3-pip python3-future git openjdk-11-jdk zip unzip python build-essential cmake git protobuf-compiler libprotobuf-dev
RUN apt -y upgrade

#Add dotnet repo
RUN mkdir -p /usr/local/sbin 
RUN wget https://download.visualstudio.microsoft.com/download/pr/e8912d3b-483b-4d6f-bd3a-3066b3194313/20f2261fe4e16e55df4bbe03c65a7648/dotnet-sdk-5.0.100-linux-arm.tar.gz;tar -zxvf dotnet-sdk-5.0.100-linux-arm.tar.gz -C /usr/local/sbin;rm dotnet-sdk-5.0.100-linux-arm.tar.gz

#Build bazel from source 
RUN mkdir -p bazel
COPY bazel-3.7.1-arm.patch /bazel/bazel-3.7.1-arm.patch
RUN cd bazel;wget https://github.com/koenvervloesem/bazel-on-arm/raw/master/patches/bazel-3.7.1-arm.patch;wget https://github.com/bazelbuild/bazel/releases/download/3.7.1/bazel-3.7.1-dist.zip;unzip bazel-3.7.1-dist.zip;patch -p1 < bazel-3.7.1-arm.patch;env EXTRA_BAZEL_ARGS="--host_javabase=@local_jdk//:jdk" bash ./compile.sh;cd ..;cp /bazel/output/bazel /usr/local/sbin/

RUN rm -rf bazel

# Set the Environment Variable for the DOTNET CLI HOME PATH
ARG dotnet_cli_home_arg=/tmp/
ENV DOTNET_CLI_HOME=$dotnet_cli_home_arg

