# ffmpeg with gpu   
   
   
## Original   
    https://developer.nvidia.com/ffmpeg
    
## Download and install ffnvcodec:
    sudo apt-get install pkgconf (ubuntu 16.04일 경우 필요)   
    git clone -b n9.0.18.3 https://github.com/FFmpeg/nv-codec-headers.git or   
    git clone https://git.videolan.org/git/ffmpeg/nv-codec-headers.git   
    cd nv-codec-headers && sudo make install && cd ..   
    sudo make install PREFIX=/usr   
    
## driver update   
        sudo add-apt-repository ppa:graphics-drivers/ppa   
        apt-cache search nvidia : 드라이버 목록 검색   
        sudo apt-get install nvidia-430   
        sudo add-apt-repository ppa:graphics-drivers/ppa   
        
## Download the latest FFmpeg 
    wget https://git.ffmpeg.org/gitweb/ffmpeg.git/snapshot/192d1d34eb3668fa27f433e96036340e1e5077a0.tar.gz    
    mv 192d1d34eb3668fa27f433e96036340e1e5077a0.tar.gz ffmpeg-4.2.2.tar.gz   
    tar -xvzf ffmpeg-4.2.2.tar.gz   

## Download and install the compatible driver from NVIDIA web site
   
### 드라이버 버전 확인   
        nvidia-smi
   
### Download and install the CUDA Toolkit CUDA toolkit   

버전확인   
    nvidia-smi : 우측 상단 CUDA 버전확인 가능   
    nvcc --version   
   
## Install util    
    sudo apt-get install nasm   
    
## Use the following configure command (Use correct CUDA library path in config command below)    
### FFmpeg 4.2.2   
    ./configure  --enable-cuda-nvcc --enable-cuvid --enable-nvenc --enable-nonfree --enable-libnpp --extra-cflags=-I/usr/local/cuda/include --extra-ldflags=-L/usr/local/cuda/lib64

### FFmpeg 4.1.5   
       ./configure --enable-cuda-sdk --enable-cuvid --enable-nvenc --enable-nonfree --enable-libnpp --extra-cflags=-I/usr/local/cuda/include --extra-ldflags=-L/usr/local/cuda/lib64
    make -j 4
   
## Use FFmpeg/libav binary as required. To start with FFmpeg, try the below sample command line for 1:2 transcoding    
    ./ffmpeg -y -hwaccel cuvid -c:v h264_cuvid -vsync 0 -i ./BigBuckBunny.mp4 -vf scale_npp=1920:1072 -vcodec h264_nvenc output0.mp4 -vf scale_npp=1280:720 -vcodec h264_nvenc output1.mp4    
   
## Other
### ssh   
#### File Download with ssh :    
    $scp ~/test.txt vas@172.17.101.233:/home/vas
#### File Upload with ssh :  
     $scp vas@106.10.33.20:/home/vas/make_file_list.sh ~/ 



