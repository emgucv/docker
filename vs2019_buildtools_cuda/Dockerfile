# escape=`

# Use the latest vs2019 buildtools
FROM emgu/vs2019_buildtools:latest

# Install CUDA
RUN powershell -command Invoke-WebRequest -UserAgent 'DockerCI' -outfile cuda_11.1.1_456.81_win10.exe https://developer.download.nvidia.com/compute/cuda/11.1.1/local_installers/cuda_11.1.1_456.81_win10.exe
RUN cuda_11.1.1_456.81_win10.exe -s nvcc_11.1 cuobjdump_11.1 nvprune_11.1 cupti_11.1 memcheck_11.1 nvdisasm_11.1 nvprof_11.1 cublas_11.1 cublas_dev_11.1 cudart_11.1 cufft_11.1 cufft_dev_11.1 curand_11.1 curand_dev_11.1 cusolver_11.1 cusolver_dev_11.1 cusparse_11.1 cusparse_dev_11.1 npp_11.1 npp_dev_11.1 nvrtc_11.1 nvrtc_dev_11.1 nvml_dev_11.1
RUN del cuda_11.1.1_456.81_win10.exe

# Copy CUDNN
# Need to download and extract CUDA DNN into the cuda folder first
ARG copy_dst="C:/Program Files/NVIDIA GPU Computing Toolkit/CUDA/v11.1/"
COPY cuda\ ${copy_dst}

# Copy Video Codec SDK
# Need to download and extract Video Codec SDK first
ARG copy_dst="C:/Program Files/NVIDIA GPU Computing Toolkit/CUDA/Video_Codec_SDK_10.0.26"
COPY Video_Codec_SDK_10.0.26 ${copy_dst}

