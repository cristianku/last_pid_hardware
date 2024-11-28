# LSTM HARDWARE PID
Hardware controlled PID using LSTM neural network


### What we need : we want to build a PID hardware controller, to control the burner of a Roasting machine.
This PID controller that takes in input a SET temperature ( desired temperature), and predict the Burner Value of . 


### Steps to achieve the desired result:

- train a LSTM neural network used for predicting the Burner value of a Hardware Pid controlled roasted machine
- Deploy the trained model to a ESP32 or similar device 

# Environment configuration

## Linux server server 
[here you can find linux server base configuration instructions](linux_configuration.md)

##### If you have a Corsair liquid cooler look here: [Corsair liquid cooler configuration](corsair_cooler.md)

##### [Maybe you are interested in configuring backups on a Truenas Server via NFS](linux_backups_truenas_nfs.md)

The server has installed two GPU, Nvidia Quadro P4000 8Gb and Nvidia quadro P6000 24Gb.
Since we dont need for this training so huge amount of memory we can use without problems the P4000 or any other Nvidia GPU.

### ANACONDA

### [Click here for a useful guide to conda commands](anaconda.pdf)

Check here the last conda download https://www.anaconda.com/download/success

#### anaconda installation
```bash
wget https://repo.anaconda.com/archive/Anaconda3-2024.10-1-Linux-x86_64.sh
chmod +x ./Anaconda3-2024.10-1-Linux-x86_64.sh
./Anaconda3-2024.10-1-Linux-x86_64.sh
```

#### anaconda environment
```bash
conda create --name deeplearning python=3.9
```

If you'd prefer that conda's base environment not be activated on startup,
   run the following command when conda is activated:
```yaml
conda config --set auto_activate_base false

```


if you get this error:
```commandline
-bash: conda: command not found
```

then Activate Anaconda:
```commandline
source ~/anaconda3/bin/activate
```

Add Anaconda to PATH
```commandline
touch ~/.bashrc
echo "export PATH=~/anaconda3/bin:\$PATH" >> ~/.bashrc
```
if the conda is still not working probably ~/.profile is missing:
```commandline
touch ~/.profile

echo "if [ -f ~/.bashrc ]; then" >> ~/.profile
echo "   source ~/.bashrc" >> ~/.profile
echo "fi" >> ~/.profile
```

initialize conda ( only once ) 
```
conda init
```

activate the new environment
```
conda activate deeplearning
```
### GIT

install git
```yaml
sudo dnf install git
```
generate ssh key, replacing the email used in the example with your GitHub email address.
```yaml
ssh-keygen -t ed25519 -C "your_email@example.com"
```
create the config file
```yaml
touch ~/.ssh/config
```

edit this file and past the following
```yaml
Host github.com
  AddKeysToAgent yes
  IdentityFile ~/.ssh/id_ed25519
```

Add the SSH public key to your account on GitHub. 

```yaml
cat ~/.ssh/id_ed25519.pub
```

For more information, 
see "[Adding a new SSH key to your GitHub account.](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)"

### Important Python libraries

#### Installing numpy
```yaml
conda install -c anaconda numpy
```

#### Installing matplotlib
```yaml
conda install -c anaconda matplotlib
```

#### Installing Pandas
```yaml
conda install -c anaconda pandas
```

#### Installing Scipy
```yaml
conda install -c anaconda scipy
```


### PYTORCH

```commandline
conda activate deeplearning

conda install -c pytorch pytorch 
```

### JUPYTER NOTEBOOK

#### Installation
```commandline
conda install -c anaconda jupyter
```

#### then you can open it with
```commandline
jupyter notebook
```
if you want Jupyter notebook to be accessible from the network instead of the local pc ( in this case its a Linux server so it doesnt have the desktop)

```commandline
jupyter notebook --ip=0.0.0.0 --no-browser
```
Lets create the configuration for Jupyter
```commandline
jupyter notebook --generate-config
```
set a password:
```commandline
jupyter notebook password
```

edit the configuration file:
```commandline
vi ~/.jupyter/jupyter_notebook_config.py
```
uncomment and set the following:
```commandline
c.NotebookApp.ip = '0.0.0.0'
c.NotebookApp.open_browser = False
c.NotebookApp.port = 8888
```

restart the notebook:
```commandline
jupyter notebook
```

#### it maybe necessary to open the port in the firewall (Fedora ):
```commandline
sudo firewall-cmd --zone=FedoraServer --add-port=8888/tcp --permanent
sudo firewall-cmd --reload

```

## REFERENCES USED
### Multi-Step LSTM Time Series Forecasting
[Python notebook](notebook/ventas-lstm-multistep.ipynb) <br>
[training data](notebook/lstm_sales_year.csv.xls) <br>

    https://www.youtube.com/watch?v=kR4TzKZBaNs&t=91s
    https://www.kaggle.com/datasets/rupakroy/lstmmultistep
