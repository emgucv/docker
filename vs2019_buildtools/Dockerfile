# escape=`

# Use the latest Windows Server Core image with .NET Framework 5.0
FROM mcr.microsoft.com/dotnet/sdk:5.0-windowsservercore-ltsc2019

# Restore the default Windows shell for correct batch processing.
SHELL ["cmd", "/S", "/C"]

# Copy our Install script.
COPY Install.cmd C:\TEMP\

# Download collect.exe in case of an install failure.
ADD https://aka.ms/vscollect.exe C:\TEMP\collect.exe

# Download the Build Tools bootstrapper.
# list of available vs2019 buildtools can be found here:
# https://docs.microsoft.com/en-us/visualstudio/releases/2019/history#release-dates-and-build-numbers
ADD https://download.visualstudio.microsoft.com/download/pr/9b3476ff-6d0a-4ff8-956d-270147f21cd4/0df5becfebf4ae2418f5fae653feebf3888b0af00d3df0415cb64875147e9be3/vs_BuildTools.exe C:\TEMP\vs_buildtools.exe

# Install Build Tools
RUN C:\TEMP\Install.cmd C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache 

# Install Build Tools
RUN C:\TEMP\Install.cmd C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache --add Microsoft.VisualStudio.Workload.VCTools

# Install Build Tools
RUN C:\TEMP\Install.cmd C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache --add Microsoft.VisualStudio.Workload.MSBuildTools

# Install Build Tools
RUN C:\TEMP\Install.cmd C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache --add Microsoft.VisualStudio.Workload.AzureBuildTools 

# Install Build Tools
RUN C:\TEMP\Install.cmd C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache --add Microsoft.VisualStudio.Workload.ManagedDesktopBuildTools

# Install Build Tools
RUN C:\TEMP\Install.cmd C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache --add Microsoft.VisualStudio.Workload.NetCoreBuildTools

# Install Build Tools
RUN C:\TEMP\Install.cmd C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache --add Microsoft.VisualStudio.Workload.UniversalBuildTools

# Install Build Tools
RUN C:\TEMP\Install.cmd C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache --add Microsoft.VisualStudio.Workload.XamarinBuildTools

# Install Build Tools
RUN C:\TEMP\Install.cmd C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache --add Microsoft.VisualStudio.Component.VC.Tools.x86.x64

# Install Build Tools
RUN C:\TEMP\Install.cmd C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache --add Microsoft.VisualStudio.Component.VC.v141.x86.x64

# Install Build Tools
RUN C:\TEMP\Install.cmd C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache --add Microsoft.VisualStudio.Component.VC.140

# Install Build Tools
RUN C:\TEMP\Install.cmd C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache --add Microsoft.VisualStudio.Component.VC.CMake.Project

# Install Build Tools
RUN C:\TEMP\Install.cmd C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache --add Microsoft.VisualStudio.ComponentGroup.UWP.VC.BuildTools

# Install Build Tools
RUN C:\TEMP\Install.cmd C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache --add Microsoft.VisualStudio.Component.Windows10SDK.18362

# Install Build Tools
RUN C:\TEMP\Install.cmd C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache --add Microsoft.Net.Component.4.8.SDK

# Install Build Tools
RUN C:\TEMP\Install.cmd C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache --add Microsoft.NetCore.Component.Runtime.5.0

# Install Build Tools
RUN C:\TEMP\Install.cmd C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache --add Microsoft.Net.ComponentGroup.4.6.1.DeveloperTools

# Install Build Tools
RUN C:\TEMP\Install.cmd C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache --add Microsoft.Net.Component.4.6.1.TargetingPack

# Install Build Tools
RUN C:\TEMP\Install.cmd C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache --add Component.OpenJDK

# Install Build Tools
RUN C:\TEMP\Install.cmd C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache --add Component.Android.SDK28

#Setup JAVA_HOME. 
ENV JAVA_HOME="C:\Program Files\Android\jdk\microsoft_dist_openjdk_1.8.0.25"

# Install Chocolatey
RUN @"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "[System.Net.ServicePointManager]::SecurityProtocol = 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"

# Install 7zip
RUN choco install -y 7zip

# Install MSYS2
RUN powershell -command Invoke-WebRequest -UserAgent 'DockerCI' -outfile msys2-x86_64-latest.tar.xz http://repo.msys2.org/distrib/msys2-x86_64-latest.tar.xz 
RUN 7z e msys2-x86_64-latest.tar.xz -Wait
RUN 7z x msys2-x86_64-latest.tar -o"C:\\" 
RUN del msys2-x86_64-latest.tar.xz msys2-x86_64-latest.tar
RUN setx path "%path%;C:\msys64\usr\bin"
# First run to setup pacman keys
RUN c:\msys64\msys2_shell.cmd -defterm -no-start
# Update all packages
RUN pacman --noconfirm -Syuu --disable-download-timeout

# Install patch command
RUN pacman --noconfirm -S patch 

#install zip 
RUN pacman --noconfirm -S zip

#install unzip 
RUN pacman --noconfirm -S unzip

#Accept ANDROID SDK licenses
RUN mkdir "C:\Program Files (x86)\Android\android-sdk\licenses"
RUN printf "\n601085b94cd77f0b54ff86406957099ebe79c4d6" > "C:\Program Files (x86)\Android\android-sdk\licenses\android-googletv-license"
RUN printf "\n859f317696f67ef3d7f30a50a5560e7834b43903" > "C:\Program Files (x86)\Android\android-sdk\licenses\android-sdk-arm-dbt-license"
RUN printf "\n24333f8a63b6825ea9c5514f83c2829b004d1fee" > "C:\Program Files (x86)\Android\android-sdk\licenses\android-sdk-license"
RUN printf "\n84831b9409646a918e30573bab4c9c91346d8abd" > "C:\Program Files (x86)\Android\android-sdk\licenses\android-sdk-preview-license"
RUN printf "\n33b6a2b64607f11b759f320ef9dff4ae5c47d97a" > "C:\Program Files (x86)\Android\android-sdk\licenses\google-gdk-license"
RUN printf "\nd975f751698a77b662f1254ddbeed3901e976f5a" > "C:\Program Files (x86)\Android\android-sdk\licenses\intel-android-extra-license"
RUN printf "\ne9acab5b5fbb560a72cfaecce8946896ff6aab9d" > "C:\Program Files (x86)\Android\android-sdk\licenses\mips-android-sysimage-license"

#update android sdk
RUN ["C:/Program Files (x86)/Android/android-sdk/tools/bin/sdkmanager.bat", "--update"]

#Install NDK
RUN ["C:/Program Files (x86)/Android/android-sdk/tools/bin/sdkmanager.bat", "ndk-bundle"]

#Install android 30
RUN ["C:/Program Files (x86)/Android/android-sdk/tools/bin/sdkmanager.bat", "platforms;android-30"]

#Install android build-tools 30
RUN ["C:/Program Files (x86)/Android/android-sdk/tools/bin/sdkmanager.bat", "build-tools;30.0.3"]

# Install python
RUN choco install -y python --version=3.8.6

# Install python wheel
RUN pip install wheel

# Install buildbot-worker
RUN pip install buildbot-worker

# Install pywin32 for buildbot-worker
RUN pip install pywin32

# Install numpy
RUN pip install numpy

# Install NSIS
RUN choco install -y nsis

# Install Sandcastle
RUN choco install -y sandcastle

# Install git
RUN choco install -y git

#install cmake
RUN choco install -y cmake

#add missing dlls to run html help workshop on ltsc2019 container
COPY itss.dll C:\Windows\SysWOW64\itss.dll
COPY itircl.dll C:\Windows\SysWOW64\itircl.dll

RUN C:\Windows\SysWOW64\regsvr32.exe /s C:\Windows\SysWOW64\itss.dll
RUN C:\Windows\SysWOW64\regsvr32.exe /s C:\Windows\SysWOW64\itircl.dll

#install emacs
RUN pacman --noconfirm -S emacs

# Copy NSIS ExecDocs plugin
# Need to download and extract NSIS ExecDocs plugin first
ARG execdos_dst="C:/Program Files (x86)/NSIS/Plugins/"
COPY ExecDos\Plugins ${execdos_dst}

# Switch to PowerShell
#SHELL ["powershell", "-command"] 

# Define the entry point for the docker container.
# This entry point starts the developer command prompt and launches the PowerShell shell.
#ENTRYPOINT ["powershell.exe", "-NoLogo", "-ExecutionPolicy", "Bypass"]