FROM l.gcr.io/google/bazel:3.1.0
RUN apt update
RUN apt -y install python3-numpy python3-pip python3-future
RUN apt -y install python-numpy python-pip python-future
RUN apt -y install android-sdk
RUN wget https://dl.google.com/android/repository/commandlinetools-linux-6609375_latest.zip -P /var/lib
RUN unzip /var/lib/commandlinetools-linux-6609375_latest.zip -d /var/lib
RUN yes | /var/lib/tools/bin/sdkmanager --sdk_root=/usr/lib/android-sdk --licenses
RUN /var/lib/tools/bin/sdkmanager --sdk_root=/usr/lib/android-sdk --update
RUN /var/lib/tools/bin/sdkmanager --sdk_root=/usr/lib/android-sdk "ndk;20.1.5948944"
RUN /var/lib/tools/bin/sdkmanager --sdk_root=/usr/lib/android-sdk "platforms;android-23"
