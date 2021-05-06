# escape=`

# Use the latest vs2019 buildtools
FROM emgu/vs2019_buildtools:16.9.4

# Install CUDA
ADD https://developer.download.nvidia.com/compute/cuda/11.3.0/network_installers/cuda_11.3.0_win10_network.exe cuda_11.3.0_win10_network.exe
#RUN powershell -command Invoke-WebRequest -UserAgent 'DockerCI' -outfile cuda_11.1.1_456.81_win10.exe https://developer.download.nvidia.com/compute/cuda/11.1.1/local_installers/cuda_11.1.1_456.81_win10.exe
RUN cuda_11.3.0_win10_network.exe -s nvcc_11.3 cuobjdump_11.3 nvprune_11.3 cupti_11.3 memcheck_11.3 nvdisasm_11.3 nvprof_11.3 cublas_11.3 cublas_dev_11.3 cudart_11.3 cufft_11.3 cufft_dev_11.3 curand_11.3 curand_dev_11.3 cusolver_11.3 cusolver_dev_11.3 cusparse_11.3 cusparse_dev_11.3 npp_11.3 npp_dev_11.3 nvrtc_11.3 nvrtc_dev_11.3 nvml_dev_11.3
RUN del cuda_11.3.0_win10_network.exe

# Copy CUDNN
# Need to download and extract CUDA DNN into the cuda folder first
ARG copy_dst="C:/Program Files/NVIDIA GPU Computing Toolkit/CUDA/v11.3/"
COPY cuda\ ${copy_dst}

# Copy Video Codec SDK
# Need to download and extract Video Codec SDK first
ARG cuda_include_dst="C:/Program Files/NVIDIA GPU Computing Toolkit/CUDA/v11.3/include/"
COPY Video_Codec_SDK_11.0.10\Interface\ ${cuda_include_dst}
ARG cuda_bin_dst="C:/Program Files/NVIDIA GPU Computing Toolkit/CUDA/v11.3/lib/"
COPY Video_Codec_SDK_11.0.10\Lib\ ${cuda_bin_dst}

