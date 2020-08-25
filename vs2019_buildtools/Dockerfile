# escape=`

# Use the latest Windows Server Core image with .NET Framework 4.8.
FROM mcr.microsoft.com/dotnet/framework/sdk:4.8-windowsservercore-ltsc2019

# Restore the default Windows shell for correct batch processing.
SHELL ["cmd", "/S", "/C"]

# Download the Build Tools bootstrapper.
# list of available vs2019 buildtools can be found here:
# https://docs.microsoft.com/en-us/visualstudio/releases/2019/history#release-dates-and-build-numbers
ADD https://download.visualstudio.microsoft.com/download/pr/067fd8d0-753e-4161-8780-dfa3e577839e/4776935864d08e66183acd5b3647c9616da989c60afbfe100d4afc459f7e5785/vs_BuildTools.exe C:\TEMP\vs_buildtools.exe

# Install Build Tools with the Microsoft.VisualStudio.Workload.AzureBuildTools workload, excluding workloads and components with known issues.
RUN C:\TEMP\vs_buildtools.exe --quiet --wait --norestart --nocache `
    --installPath C:\BuildTools `
    --add Microsoft.VisualStudio.Workload.AzureBuildTools `
	--add Microsoft.Net.Component.4.6.1.TargetingPack `
	--add Microsoft.Net.ComponentGroup.4.6.1.DeveloperTools `
	--add Microsoft.VisualStudio.Workload.ManagedDesktopBuildTools `
	--add Microsoft.VisualStudio.Workload.MSBuildTools `
	--add Microsoft.VisualStudio.Workload.NetCoreBuildTools `
	--add Microsoft.VisualStudio.Workload.UniversalBuildTools `
	--add Microsoft.VisualStudio.Workload.VCTools `
	--add Microsoft.VisualStudio.Component.VC.CMake.Project `
	--add Microsoft.VisualStudio.Component.VC.Tools.x86.x64 `
	--add Microsoft.VisualStudio.ComponentGroup.UWP.VC.BuildTools `
	--add Microsoft.VisualStudio.Component.Windows10SDK.18362 `
	--add Microsoft.Net.Component.4.8.SDK `
	--add Microsoft.VisualStudio.Workload.XamarinBuildTools `
	--add Component.Android.SDK28 `
	--add Component.OpenJDK `
    --remove Microsoft.VisualStudio.Component.Windows10SDK.10240 `
    --remove Microsoft.VisualStudio.Component.Windows10SDK.10586 `
    --remove Microsoft.VisualStudio.Component.Windows10SDK.14393 `
    --remove Microsoft.VisualStudio.Component.Windows81SDK `
 || IF "%ERRORLEVEL%"=="3010" EXIT 0

# Install Chocolatey
RUN @"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "[System.Net.ServicePointManager]::SecurityProtocol = 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"

# Install python
RUN choco install -y python

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

# Install 7zip
RUN choco install -y 7zip

# Switch to PowerShell
#SHELL ["powershell", "-command"] 

# Install MSYS2
#RUN choco install -y msys2 --version 20200602.0.0
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

# Define the entry point for the docker container.
# This entry point starts the developer command prompt and launches the PowerShell shell.
ENTRYPOINT ["powershell.exe", "-NoLogo", "-ExecutionPolicy", "Bypass"]