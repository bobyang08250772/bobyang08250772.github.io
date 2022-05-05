1.Install dependencies
  {% include codeHeader.html %}
  ``` 
  yum -y install epel-release
  ```
  
  {% include codeHeader.html %}
  ```
  yum -y install gcc binutils wget
  ```
  {% include codeHeader.html %}
  ```
  yum -y install kernel-devel 
  ```

2.Deactivate nouveau

  2.1 Check if nouveau is open
  
  {% include codeHeader.html %}
  ```
  lsmod | grep nouveau
  ```

  **Note**：No output means it is closed, jump to step 3

  2.2. Change configuration
  
  {% include codeHeader.html %}
  ```
  echo -e "blacklist nouveau\noptions nouveau modeset=0" > /etc/modprobe.d/blacklist.conf
  ```

  2.3. Backup Img

  {% include codeHeader.html %}
  ```
  mv /boot/initramfs-$(uname -r).img /boot/initramfs-$(uname -r).img.bak
  ```

  2.4.Rebuild

  {% include codeHeader.html %}
  ```
  dracut /boot/initramfs-$(uname -r).img $(uname -r)
  ```

  2.5.Reboot your server

  {% include codeHeader.html %}
  ```
  reboot
  ```

  2.6. Check if nouveau is closed
  
  {% include codeHeader.html %}
  ```
  lsmod | grep nouveau
  ```

  **Note**：No output means it is closed；

3.Check driver

  3.1.install elrepo
  
  {% include codeHeader.html %}
  ```
  rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
  ```
  
  {% include codeHeader.html %}
  ```
  rpm -Uvh http://www.elrepo.org/elrepo-release-7.0-4.el7.elrepo.noarch.rpm
  ```

  or
  
  {% include codeHeader.html %}
  ```
  yum -y install https://www.elrepo.org/elrepo-release-7.0-4.el7.elrepo.noarch.rpm
  ```

  3.2.Install nvidia-detect
  
  {% include codeHeader.html %}
  ```
  yum -y install nvidia-detect
  ```

  3.3.Detect version 

  {% include codeHeader.html %}
  ```
  nvidia-detect -v
  ```
  Output
  ```
  This device requires the current 440.36 NVIDIA driver kmod-nvidia
  ```

4.Install Driver

  4.1. Download Driver
  
  {% include codeHeader.html %}
  ```
  wget https://us.download.nvidia.cn/XFree86/Linux-x86_64/440.36/NVIDIA-Linux-x86_64-440.36.run
  ```

  **Note**: if you don't have my current version or don't know the download url, check on the offcial website [go](https://www.nvidia.com/Download/index.aspx)

  Here you can choose a driver according to your GPU
  
  <img  width="559" alt="image" src="https://user-images.githubusercontent.com/87290044/165709160-9151af5a-2fb7-443b-9c2e-77975d739f6b.png">



  4.2. Authorize

  {% include codeHeader.html %}
  ```
  chmod +x NVIDIA-Linux-x86_64-440.36.run
  ```

  4.3. Install

  {% include codeHeader.html %}
  ```
  sh ./NVIDIA-Linux-x86_64-440.36.run -s
  ```

  ###Check info###
  
  {% include codeHeader.html %}
  ```
  nvidia-smi
  ```
  
  Output
  <img width="559" alt="image" src="https://user-images.githubusercontent.com/87290044/165708058-b2a314e1-fcc8-4d2b-a978-0c715f7ae3a0.png">

5.Uninstall 

  5.1.Uninstall NVIDIA
  
  {% include codeHeader.html %}
  ```
  nvidia-uninstall
  ```

  5.2. Clean up

  {% include codeHeader.html %}
  ```
  dkms remove
  ```

  **Note**：use "yum -y install dkms" to install dkms


