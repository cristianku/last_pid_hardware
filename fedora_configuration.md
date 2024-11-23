# last_pid_hardware
Hardware controlled PID using LSTM neural network

### What we need : we want to build a PID hardware controller, to control the burner of a Roasting machine.
This PID controller that takes in input a SET temperature ( desired temperature), and predict the Burner Value of . 


### Steps to achieve the desired result:

- train a LSTM neural network used for predicting the Burner value of a Hardware Pid controlled roasted machine
- Deploy the trained model to a ESP32 or similar device 

# Environment configuration

## Fedora 41 server with 
[here you can find fedora configuration instruction](fedora_configuration.md)

The server has installed two GPU, Nvidia Quadro P4000 8Gb and Nvidia quadro P6000 24Gb
Since we dont need for this training so huge amount of memory we can use without problems the P4000 or any other Nvidia GPU.

### CONDA
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh

### PYTORCH


