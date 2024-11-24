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

### CONDA
```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```

### PYTORCH

## REFERENCES USED
### Multi-Step LSTM Time Series Forecasting
[Python notebook](notebook/ventas-lstm-multistep.ipynb) <br>
[training data](notebook/lstm_sales_year.csv.xls) <br>

    https://www.youtube.com/watch?v=kR4TzKZBaNs&t=91s
    https://www.kaggle.com/datasets/rupakroy/lstmmultistep
