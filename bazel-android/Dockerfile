FROM ubuntu:22.04

RUN apt update

#Add basic packages required to install bazel and dotnet repo
RUN apt -y install curl wget gnupg apt-transport-https

#Add bazel repo
COPY bazel.list /etc/apt/sources.list.d/bazel.list
RUN wget https://bazel.build/bazel-release.pub.gpg 
RUN apt-key add bazel-release.pub.gpg

#Add dotnet repo
RUN wget https://packages.microsoft.com/config/ubuntu/22.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb 
RUN dpkg -i packages-microsoft-prod.deb

RUN apt update

RUN apt -y install openjdk-18-jdk
RUN apt -y install python3-numpy python3-pip python3-future python-is-python3
RUN apt -y install android-sdk
RUN apt -y install build-essential cmake cmake-curses-gui git protobuf-compiler libprotobuf-dev

RUN wget https://dl.google.com/android/repository/commandlinetools-linux-8092744_latest.zip -P /var/lib/android-sdk
RUN unzip -o /var/lib/android-sdk/commandlinetools-linux-8092744_latest.zip -d /var/lib/android-sdk
RUN yes | /var/lib/android-sdk/cmdline-tools/bin/sdkmanager --sdk_root=/usr/lib/android-sdk --licenses
RUN /var/lib/android-sdk/cmdline-tools/bin/sdkmanager --sdk_root=/usr/lib/android-sdk --update
RUN /var/lib/android-sdk/cmdline-tools/bin/sdkmanager --sdk_root=/usr/lib/android-sdk "ndk-bundle"
RUN /var/lib/android-sdk/cmdline-tools/bin/sdkmanager --sdk_root=/usr/lib/android-sdk --install "ndk;21.4.7075529"
#RUN /var/lib/android-sdk/cmdline-tools/bin/sdkmanager --sdk_root=/usr/lib/android-sdk "platforms;android-31"
RUN /var/lib/android-sdk/cmdline-tools/bin/sdkmanager --sdk_root=/usr/lib/android-sdk "platforms;android-32"

RUN apt -y upgrade

RUN apt -y install dotnet-sdk-6.0 aspnetcore-runtime-6.0

# Install the lsb-release package to help identify platform.
RUN apt -y install lsb-release 

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

# Install packages for building Emgu CV
RUN apt-get -y install libgtk-3-dev libgstreamer1.0-dev libavcodec-dev libswscale-dev libavformat-dev libv4l-dev libdc1394-dev ocl-icd-dev freeglut3-dev libgeotiff-dev libusb-1.0-0-dev 

# Install packages needed by bazel when compiling tensorflow
RUN apt-get -y install llvm

# Install bazel
RUN apt -y install bazel=5.0.0