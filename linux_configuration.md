# LSTM HARDWARE PID - LINUX CONF FOR DEEP LEARNING
Hardware controlled PID using LSTM neural network

# FEDORA 39
These are general configurations for Fedora (41) that can be applied to any Deep Learning project

### FEDORA is installed on a Raid 1 SSD ( two SSD, 1 in mirroring)

### NVIDIA INSTALLATION

Add Nvidia Repository
```bash
sudo dnf config-manager --add-repo https://developer.download.nvidia.com/compute/cuda/repos/fedora39/x86_64/cuda-fedora39.repo
```
In Fedora 41:
```commandline
sudo dnf5 config-manager addrepo --from-repofile=https://developer.download.nvidia.com/compute/cuda/repos/fedora39/x86_64/cuda-fedora39.repo
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

### PREPARING NVME DRIVES

##### Creating a partition
```bash
sudo mkfs.ext4 /dev/nvme0n1p1

sudo parted /dev/nvme0n1 --script mklabel gpt
sudo parted /dev/nvme0n1 --script mkpart primary ext4 0% 100%
sudo mkfs.ext4 /dev/nvme0n1p1

sudo parted /dev/nvme1n1 --script mklabel gpt
sudo parted /dev/nvme1n1 --script mkpart primary ext4 0% 100%
sudo mkfs.ext4 /dev/nvme1n1p1

cristianku@serverone-deep:~$ lsblk |grep nvme
nvme0n1     259:0    0   1.8T  0 disk  
└─nvme0n1p1 259:2    0   1.8T  0 part  
nvme1n1     259:1    0 931.5G  0 disk  
└─nvme1n1p1 259:4    0 931.5G  0 part 
```

##### Moving home to nvme
```commandline
sudo mkdir /mnt/new_home
sudo mount /dev/nvme0n1p1 /mnt/new_home
sudo mv /home /mnt/home_new
sudo mkdir cristianku

sudo cp /etc/fstab /etc/fstab.bak
```
add this to /etc/fstab:
```commandline
/dev/nvme0n1p1 /home ext4 defaults 0 2
```
check if correctly mounted:
```commandline
cristianku@localhost:~$ df -h | grep /home
/dev/nvme0n1p1  1.8T  2.1M  1.7T   1% /home
```
change the ownership:
```commandline
sudo chown -R cristianku:cristianku /home/cristianku
```
lets check the available space and the mounted nvme:
```commandline
cristianku@localhost:~$ df -h /home/cristianku
Filesystem      Size  Used Avail Use% Mounted on
/dev/nvme0n1p1  1.8T  2.1M  1.7T   1% /home
cristianku@localhost:~$ 
```

##### Getting the BLKID
```bash
cristianku@serverone-deep:~$ sudo blkid /dev/nvme0n1p1
/dev/nvme0n1p1: PARTLABEL="primary" PARTUUID="86f602aa-ae12-4cd9-aa3c-9ca74816e3c1"

cristianku@serverone-deep:~$ sudo blkid /dev/nvme1n1p1
/dev/nvme1n1p1: PARTLABEL="primary" PARTUUID="ca63c21a-f5ff-46a0-a2e9-e961a89ec0a2"
```

#### Mounting NVME
```bash
sudo mkdir -p /mnt/nvme0
sudo mkdir -p /mnt/nvme1

sudo vi /etc/fstab
UUID=<UUID-for-nvme0n1p1> /mnt/nvme0 ext4 defaults 0 2
UUID=<UUID-for-nvme1n1p1> /mnt/nvme1 ext4 defaults 0 2

sudo mount -a

```