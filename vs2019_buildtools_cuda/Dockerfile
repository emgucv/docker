# escape=`

# Use the latest vs2019 buildtools
FROM emgu/vs2019_buildtools:latest

# Install CUDA
RUN powershell -command Invoke-WebRequest -UserAgent 'DockerCI' -outfile cuda_11.0.3_451.82_win10.exe https://developer.download.nvidia.com/compute/cuda/11.0.3/local_installers/cuda_11.0.3_451.82_win10.exe
RUN cuda_11.0.3_451.82_win10.exe -s nvcc_11.0 cuobjdump_11.0 nvprune_11.0 memcheck_11.0 nvdisasm_11.0 nvprof_11.0 cublas_11.0 cublas_dev_11.0 cudart_11.0 cufft_11.0 cufft_dev_11.0 curand_11.0 curand_dev_11.0 cusolver_11.0 cusolver_dev_11.0 cusparse_11.0 cusparse_dev_11.0 npp_11.0 npp_dev_11.0 nvrtc_11.0 nvrtc_dev_11.0 nvml_dev_11.0
RUN del cuda_11.0.3_451.82_win10.exe

# Copy CUDNN
# Need to download and extract CUDA DNN into the cuda folder first
ARG copy_dst="C:/Program Files/NVIDIA GPU Computing Toolkit/CUDA/v11.0/"
COPY cuda\ ${copy_dst}

#Setup JAVA_HOME. 
#TODO: Should move it to vs2019_buildtools\Dockerfile
ENV JAVA_HOME="C:\Program Files\Android\jdk\microsoft_dist_openjdk_1.8.0.25"

#Accept ANDROID SDK licenses
RUN mkdir "C:\Program Files (x86)\Android\android-sdk\licenses"
RUN printf "\n601085b94cd77f0b54ff86406957099ebe79c4d6" > "C:\Program Files (x86)\Android\android-sdk\licenses\android-googletv-license"
RUN printf "\n859f317696f67ef3d7f30a50a5560e7834b43903" > "C:\Program Files (x86)\Android\android-sdk\licenses\android-sdk-arm-dbt-license"
RUN printf "\n24333f8a63b6825ea9c5514f83c2829b004d1fee" > "C:\Program Files (x86)\Android\android-sdk\licenses\android-sdk-license"
RUN printf "\n84831b9409646a918e30573bab4c9c91346d8abd" > "C:\Program Files (x86)\Android\android-sdk\licenses\android-sdk-preview-license"
RUN printf "\n33b6a2b64607f11b759f320ef9dff4ae5c47d97a" > "C:\Program Files (x86)\Android\android-sdk\licenses\google-gdk-license"
RUN printf "\nd975f751698a77b662f1254ddbeed3901e976f5a" > "C:\Program Files (x86)\Android\android-sdk\licenses\intel-android-extra-license"
RUN printf "\ne9acab5b5fbb560a72cfaecce8946896ff6aab9d" > "C:\Program Files (x86)\Android\android-sdk\licenses\mips-android-sysimage-license"

#Install NDK
RUN ["C:/Program Files (x86)/Android/android-sdk/tools/bin/sdkmanager.bat", "ndk-bundle"]

#update android sdk
RUN ["C:/Program Files (x86)/Android/android-sdk/tools/bin/sdkmanager.bat", "--update"]

#install cmake
RUN choco install -y cmake

#install zip 
RUN pacman --noconfirm -S zip

#install unzip 
RUN pacman --noconfirm -S unzip