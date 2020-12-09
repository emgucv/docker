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

RUN wget https://dl.google.com/android/repository/commandlinetools-linux-6609375_latest.zip -P /var/lib/android-sdk
RUN unzip -o /var/lib/android-sdk/commandlinetools-linux-6609375_latest.zip -d /var/lib/android-sdk
RUN yes | /var/lib/android-sdk/tools/bin/sdkmanager --sdk_root=/usr/lib/android-sdk --licenses
RUN /var/lib/android-sdk/tools/bin/sdkmanager --sdk_root=/usr/lib/android-sdk --update
RUN /var/lib/android-sdk/tools/bin/sdkmanager --sdk_root=/usr/lib/android-sdk "ndk-bundle"
RUN /var/lib/android-sdk/tools/bin/sdkmanager --sdk_root=/usr/lib/android-sdk "platforms;android-30"

RUN apt -y upgrade

RUN apt -y install dotnet-sdk-5.0 aspnetcore-runtime-5.0

RUN apt -y install bazel=3.7.0

RUN mkdir /tmp/build_output

# Set the Environment Variable for the DOTNET CLI HOME PATH
ARG dotnet_cli_home_arg=/tmp/
ENV DOTNET_CLI_HOME=$dotnet_cli_home_arg

# Install emsdk
RUN git clone https://github.com/emscripten-core/emsdk.git
RUN emsdk/emsdk install latest
# Added permission for none-root user to use emsdk
RUN chmod -R ug+rw emsdk
RUN chmod -R a+rw emsdk/upstream/emscripten/cache
