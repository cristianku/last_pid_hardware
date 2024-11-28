# LSTM HARDWARE PID - LINUX CONF FOR DEEP LEARNING
Hardware controlled PID using LSTM neural network

# FEDORA 39
These are general configurations for Fedora (41) that can be applied to any Deep Learning project

##### If you have a Corsair liquid cooler look here:
[Corsair liquid cooler configuration](corsair_cooler.md)


### FEDORA is installed on a Raid 1 SSD ( two SSD, 1 in mirroring)

### NVIDIA INSTALLATION

Add Nvidia Repository
```bash
sudo dnf config-manager --add-repo https://developer.download.nvidia.com/compute/cuda/repos/fedora40/x86_64/cuda-fedora40.repo
```
verify :
```commandline
cat /etc/yum.repos.d/cuda-fedora39.repo

```
Continue the installation
```bash
sudo dnf update
sudo dnf clean all
sudo dnf -y module install nvidia-driver:latest-dkms

sudo dnf -y install cuda
sudo dnf -y install cuda-toolkit
````
### NVIDIA COOLER CONTROL
#### Its important to note that the fan control maybe not be working enough, so we emphatize to install this software to control better the cooling of your Nvidia 

#### Installing Cooler Control https://gitlab.com/coolercontrol/coolercontrol
[nvidia_cooler_control.md](Here the instructions how to install the Nvidia Cooler control)


### PREPARING NVME DRIVES
#### Use a different disk for container storage
```commandline
sudo mkfs.ext4 /dev/nvme1n1
sudo mkdir /mnt/nvme1
sudo mount /dev/nvme1n1 /mnt/nvme1
echo "/dev/nvme1n1 /mnt/nvme1 ext4 defaults 0 0" | sudo tee -a /etc/fstab
```
