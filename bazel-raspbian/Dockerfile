FROM balenalib/raspberrypi3-debian:latest

RUN apt update

#Add basic packages required to install bazel and dotnet repo
RUN apt -y install curl wget gnupg apt-transport-https

RUN apt -y install openjdk-8-jdk
RUN apt -y install python3-numpy python3-pip python3-future 
RUN apt -y install build-essential cmake git protobuf-compiler libprotobuf-dev
RUN apt -y upgrade

#Add dotnet repo
RUN wget https://download.visualstudio.microsoft.com/download/pr/e8912d3b-483b-4d6f-bd3a-3066b3194313/20f2261fe4e16e55df4bbe03c65a7648/dotnet-sdk-5.0.100-linux-arm.tar.gz
RUN mkdir -p /usr/local/sbin 
RUN tar -zxvf dotnet-sdk-5.0.100-linux-arm.tar.gz -C /usr/local/sbin

#Add bazel repo
RUN apt -y install git openjdk-11-jdk zip unzip
RUN mkdir -p bazel;cd bazel;wget https://github.com/bazelbuild/bazel/releases/download/3.7.1/bazel-3.7.1-dist.zip;unzip bazel-3.7.1-dist.zip;env EXTRA_BAZEL_ARGS="--host_javabase=@local_jdk//:jdk --host_jvm_args=-Xmx2g --discard_analysis_cache --nokeep_state_after_build --notrack_incremental_state" bash ./compile.sh;cd ..

#COPY bazel.list /etc/apt/sources.list.d/bazel.list
#RUN wget https://bazel.build/bazel-release.pub.gpg 
#RUN apt-key add bazel-release.pub.gpg
#RUN apt -y install bazel=3.7.0

# Set the Environment Variable for the DOTNET CLI HOME PATH
ARG dotnet_cli_home_arg=/tmp/
ENV DOTNET_CLI_HOME=$dotnet_cli_home_arg

