# escape=`

# Use the latest vs2019 buildtools with cuda
FROM emgu/vs2019_buildtools_cuda:cuda_11.1.1

# Based on the instructions from https://docs.openvinotoolkit.org/latest/openvino_docs_install_guides_installing_openvino_docker_windows.html
# Copy OpenVino
# Need to download openvino installer first
ADD https://registrationcenter-download.intel.com/akdlm/irc_nas/17505/w_openvino_toolkit_p_2021.2.185.exe w_openvino_toolkit_p_2021.2.185.exe

# Install OpenVino
#RUN powershell.exe -Command Start-Process 'w_openvino_toolkit_p_2021.2.185.exe' -ArgumentList '--s --a install --eula=accept --output=openvino_install_out.log --components=OPENVINO_COMMON,INFERENCE_ENGINE,INFERENCE_ENGINE_SDK,INFERENCE_ENGINE_SAMPLES,OMZ_TOOLS,POT,INFERENCE_ENGINE_CPU,INFERENCE_ENGINE_GPU,MODEL_OPTIMIZER,OMZ_DEV,OPENCV_PYTHON,OPENCV_RUNTIME,OPENCV,DOCS,SETUPVARS,VC_REDIST_2017_X64,icl_redist' -Wait
RUN powershell.exe -Command Start-Process 'w_openvino_toolkit_p_2021.2.185.exe' -ArgumentList '--s --a install --eula=accept --output=openvino_install_out.log' -Wait
RUN del w_openvino_toolkit_p_2021.2.185.exe

# Copy MediaFeaturePack
# Need to download openvino installer first
COPY Windows_MediaFeaturePack_x64_1903_V1.msu Windows_MediaFeaturePack_x64_1903_V1.msu

# Install MediaFeaturePack
RUN powershell.exe -command Start-Process Windows_MediaFeaturePack_x64_1903_V1.msu -ArgumentList '/quiet' -Wait
RUN del Windows_MediaFeaturePack_x64_1903_V1.msu
