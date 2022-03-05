FROM debian:bullseye-backports

RUN apt update
RUN apt -y upgrade

#Add packages required to install bazel and dotnet repo
RUN apt -y install curl wget gnupg apt-transport-https python3-numpy python3-pip python3-future git openjdk-17-jdk zip unzip python build-essential cmake git protobuf-compiler libprotobuf-dev libusb-1.0-0-dev libgeotiff-dev freeglut3-dev lsb-release

#Add dotnet repo
RUN mkdir -p /usr/local/sbin 
RUN wget https://download.visualstudio.microsoft.com/download/pr/1f85b038-9917-4d0a-8485-5dc86510eec7/a7555924fe292c6c2140893f066abe65/dotnet-sdk-6.0.100-linux-arm.tar.gz;tar -zxvf dotnet-sdk-6.0.100-linux-arm.tar.gz -C /usr/local/sbin;rm dotnet-sdk-6.0.100-linux-arm.tar.gz

#Build bazel from source 
RUN mkdir -p bazel

#Download from https://github.com/koenvervloesem/bazel-on-arm/tree/master/patches
RUN cd bazel;wget https://github.com/koenvervloesem/bazel-on-arm/raw/master/patches/bazel-4.2.1-arm.patch;wget https://github.com/bazelbuild/bazel/releases/download/4.2.1/bazel-4.2.1-dist.zip;unzip bazel-4.2.1-dist.zip;patch -p1 < bazel-4.2.1-arm.patch;env EXTRA_BAZEL_ARGS="--host_javabase=@local_jdk//:jdk" BAZEL_JAVAC_OPTS="-J-Xms384m -J-Xmx800m" JAVA_TOOL_OPTS="-Xmx800m" bash ./compile.sh;cd ..;cp /bazel/output/bazel /usr/local/sbin/

RUN rm -rf bazel

# Set the Environment Variable for the DOTNET CLI HOME PATH
ARG dotnet_cli_home_arg=/tmp/
ENV DOTNET_CLI_HOME=$dotnet_cli_home_arg

