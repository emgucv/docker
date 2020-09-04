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

# Copy Video Codec SDK
# Need to download and extract Video Codec SDK first
ARG copy_dst="C:/Program Files/NVIDIA GPU Computing Toolkit/CUDA/Video_Codec_SDK_10.0.26"
COPY Video_Codec_SDK_10.0.26 ${copy_dst}

