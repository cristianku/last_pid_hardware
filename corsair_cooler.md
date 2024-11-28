# CORSAIR COOLER CONFIGURATION
##### Corsair iCUE H100i ELITE RGB Liquid CPU Cooler

### Install liquidctl:
```commandline
sudo dnf install liquidctl
```
then get the list:
```commandline
liquidctl list

cristianku@localhost:~$ liquidctl list
Device #0: Corsair iCUE H100i Elite RGB (experimental)
Device #1: Gigabyte RGB Fusion 2.0 5702 Controller
cristianku@localhost:~$ 

```
Assuming that the first one is the controller for the liquidcooler fans :
```bash
sudo liquidctl --device 0 initialize
```

### Creating the script for a Balanced profile 
Assuming that you have fans on the front and on the back of the cooler:
```yaml
sudo liquidctl --match "Corsair iCUE H100i Elite RGB" initialize --pump-mode balanced
sudo liquidctl --match "Corsair iCUE H100i Elite RGB" set fan1 speed 60
sudo liquidctl --match "Corsair iCUE H100i Elite RGB" set fan2 speed 60

```

### Automatically run this script at startup on your Fedora server

#### create the script
```bash
sudo vi /usr/local/bin/liquidctl_startup.sh
```

#### Add the following to the file:
```bash
#!/bin/bash
sudo liquidctl --match "Corsair iCUE H100i Elite RGB" initialize --pump-mode balanced
sudo liquidctl --match "Corsair iCUE H100i Elite RGB" set fan1 speed 70
sudo liquidctl --match "Corsair iCUE H100i Elite RGB" set fan2 speed 70
```
Save and exit the editor.

#### Make the Script Executable
```bash
sudo chmod +x /usr/local/bin/liquidctl_startup.sh
```
#### Create a Systemd Service
```bash
sudo vi /etc/systemd/system/liquidctl.service
```
add the following lines
```
[Unit]
Description=Liquidctl Initialization Service
After=multi-user.target

[Service]
Type=oneshot
ExecStart=/usr/local/bin/liquidctl_startup.sh
RemainAfterExit=true

[Install]
WantedBy=multi-user.target
```

#### Reload Systemd and Enable the Service

```bash
sudo systemctl daemon-reload
```
Enable the service to start at boot:
```bash
sudo systemctl enable liquidctl.service
```

#### Check the cooler settings and status
```bash
sudo liquidctl --device 0 status
```
```
WARNING: -d/--device is deprecated, prefer --match or other selection options
Corsair iCUE H100i Elite RGB (experimental)
├── Liquid temperature    26.2  °C
├── Fan 1 speed           1327  rpm
├── Fan 1 duty              60  %
├── Fan 2 speed           1004  rpm
├── Fan 2 duty              60  %
├── Pump speed            2505  rpm
└── Pump duty               75  %
```