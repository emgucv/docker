# escape=`

# Use the latest vs2019 buildtools
FROM emgu/vs2019_buildtools:16.11.0

# Install CUDA
ADD https://developer.download.nvidia.com/compute/cuda/11.4.1/network_installers/cuda_11.4.1_win10_network.exe cuda_11.4.1_win10_network.exe

#RUN powershell -command Invoke-WebRequest -UserAgent 'DockerCI' -outfile cuda_11.1.1_456.81_win10.exe https://developer.download.nvidia.com/compute/cuda/11.1.1/local_installers/cuda_11.1.1_456.81_win10.exe
RUN cuda_11.4.1_win10_network.exe -s nvcc_11.4 cuobjdump_11.4 nvprune_11.4 cupti_11.4 memcheck_11.4 nvdisasm_11.4 nvprof_11.4 cublas_11.4 cublas_dev_11.4 cudart_11.4 cufft_11.4 cufft_dev_11.4 curand_11.4 curand_dev_11.4 cusolver_11.4 cusolver_dev_11.4 cusparse_11.4 cusparse_dev_11.4 npp_11.4 npp_dev_11.4 nvrtc_11.4 nvrtc_dev_11.4 nvml_dev_11.4
RUN del cuda_11.4.1_win10_network.exe

# Copy CUDNN
# Need to download and extract CUDA DNN into the cuda folder first
ARG copy_dst="C:/Program Files/NVIDIA GPU Computing Toolkit/CUDA/v11.4/"
COPY cuda\ ${copy_dst}

# Copy Video Codec SDK
# Need to download and extract Video Codec SDK first
ARG cuda_include_dst="C:/Program Files/NVIDIA GPU Computing Toolkit/CUDA/v11.4/include/"
COPY Video_Codec_SDK_11.1.5\Interface\ ${cuda_include_dst}
ARG cuda_bin_dst="C:/Program Files/NVIDIA GPU Computing Toolkit/CUDA/v11.4/lib/"
COPY Video_Codec_SDK_11.1.5\Lib\ ${cuda_bin_dst}

