FROM ubuntu:20.04

RUN apt update

#Add basic packages required to install bazel and dotnet repo
RUN apt -y install curl wget gnupg apt-transport-https

#Add bazel repo
COPY bazel.list /etc/apt/sources.list.d/bazel.list
RUN wget https://bazel.build/bazel-release.pub.gpg 
RUN apt-key add bazel-release.pub.gpg

#Add dotnet repo
RUN wget https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
RUN dpkg -i packages-microsoft-prod.deb

RUN apt update

RUN apt -y install openjdk-8-jdk
RUN apt -y install python3-numpy python3-pip python3-future python-is-python3
RUN apt -y install android-sdk
RUN apt -y install build-essential cmake git protobuf-compiler libprotobuf-dev
RUN apt -y upgrade

RUN apt -y install dotnet-sdk-3.1 aspnetcore-runtime-3.1

RUN apt -y install bazel=3.1.0

RUN wget https://dl.google.com/android/repository/commandlinetools-linux-6609375_latest.zip -P /var/lib
RUN unzip /var/lib/commandlinetools-linux-6609375_latest.zip -d /var/lib
RUN yes | /var/lib/tools/bin/sdkmanager --sdk_root=/usr/lib/android-sdk --licenses
RUN /var/lib/tools/bin/sdkmanager --sdk_root=/usr/lib/android-sdk --update
RUN /var/lib/tools/bin/sdkmanager --sdk_root=/usr/lib/android-sdk "ndk;20.1.5948944"
RUN /var/lib/tools/bin/sdkmanager --sdk_root=/usr/lib/android-sdk "platforms;android-23"

RUN mkdir /tmp/build_output

# Set the Environment Variable for the DOTNET CLI HOME PATH
ARG dotnet_cli_home_arg=/tmp/
ENV DOTNET_CLI_HOME=$dotnet_cli_home_arg