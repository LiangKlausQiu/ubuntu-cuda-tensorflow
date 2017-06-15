# ubuntu 16.04.2 LTS + cuda 8.0 + cudnn v6.0 + tensorflow installation guide
### Windows10 + ubuntu 16.04.2 dual boot installtion see http://www.jianshu.com/p/2eebd6ad284d.  
Note:  
* Disable fast boot and secure boot (Bios -> boot -> secure boot -> key management -> clear key);   
* Give /boot more space, maybe 1 GB;   
* Don't use EasyBCD.  
  
### ubuntu 16.04.2 + cuda 8.0 + cudnn v6.0 installtion see http://blog.csdn.net/autocyz/article/details/52299889.  
* install nvidia driver  
1. check your driver on http://www.nvidia.com/Download/index.aspx?lang=en-us  
2. sudo add-apt-repository ppa:graphics-drivers/ppa  
   sudo apt-get update  
	 sudo apt-get install nvidia-375 #your driver  
	 sudo apt-get install mesa-common-dev  
	 sudo apt-get install freeglut3-dev  
	 sudo reboot    
	 nvidia-smi  
	 nvidia-settings  
* install cuda
  download cuda from https://developer.nvidia.com/cuda-release-candidate-download  
	sudo sh cuda_8.0.27_linux.run #your cuda runfile name
  sudo vim ~/.bashrc, add the following lines:  
  export PATH=/usr/local/cuda/bin${PATH:+:${PATH}}  
  export LD_LIBRARY_PATH=/usr/local/cuda/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
  sudo vim /etc/profile, add:   
  export PATH=/usr/local/cuda/bin:$PATH
  sudo vim /etc/ld.so.conf.d/cuda.conf, add:  
  /usr/local/cuda/lib64
	sudo ldconfig  
  if error 'libEGL.so.1 is not a symbolic link ...', then    
  sudo mv /usr/lib/nvidia-375/libEGL.so.1 /usr/lib/nvidia-375/libEGL.so.1.org
  sudo mv /usr/lib32/nvidia-375/libEGL.so.1 /usr/lib32/nvidia-375/libEGL.so.1.org
  sudo ln -s /usr/lib/nvidia-375/libEGL.so.375.66 /usr/lib/nvidia-375/libEGL.so.1
  sudo ln -s /usr/lib32/nvidia-375/libEGL.so.375.66 /usr/lib32/nvidia-375/libEGL.so.1  
  sudo ldconfig
  test cuda samples:
  cd /usr/local/cuda-7.5/samples/1_Utilities/deviceQuery
  sudo make
  sudo ./deviceQuery
	* install cudnn
	download cudnn from https://developer.nvidia.com/cudnn to ~/Downloads/
  cd ~/Downloads/cuda/include/
  sudo cp cudnn.h /usr/local/cuda/include/
  cd ~/Downloads/cuda/lib64/
  sudo cp lib* /usr/local/cuda/lib64/    
  cd /usr/local/cuda/lib64/ 
  sudo ln -s libcudnn.so.6.* libcudnn.so.5
