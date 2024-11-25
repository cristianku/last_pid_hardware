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

### PYTORCH

```commandline
conda activate deeplearning

conda install -c pytorch pytorch 

conda deactivate deeplearning
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
