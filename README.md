# Cybersecurity Honeypot: fighting ransomware with sentinel files

**TUTTO IL MATERIALE UTILE E' IN TESTFOLDER, PER ORA, PER EVITARE DI CREARE FILE RANDOM DAPPERTUTTO !** <br /> 
Ho aggiunto delle parti non testate a rpiClient.py e pubsub.py, potrebbero non funzionare.

## Introduction

This is the project of 'Cybersecurity for Embedded Systems' course @PoliTO, A.Y. 2021-2022. <br /><br />
We present a cluster of Raspberry Pi devices. Each raspberry can communicate to the others in the network, according to the principles of a fully connected mesh. <br /><br />
The following picture is a schematic of our proposed solution: <br /><br /> 
![Schematic](/images/malwareHoneypot.drawio.png) <br /><br /> 
Honeypot services are distributed to each node in the cluster. Each node performs a scan of its own file system, looking for some uncostistency in the hash values of sentinel files. Sentinel files are special files that do not provide production value and therefore each interaction with them (for instance, an update of their content) must be considered malicious.<br />
If an attack is spotted, the node under attack notifies all other nodes in the cluster with a MQTT message and they start ignoring messages coming from the infected node. This avoids the spread of the malware attack across the cluster.<br />
Once the node is declared as infected, we perform a shutdown and we suppose that a technician will restore the node. After an interval of period, the new message from the node is managed as benign.

## Deployment Steps

1) Launch the command ```python --version```. If the version is below 3.X.X, then perform step #2, otherwise skip to step #3;
2) Install Python3 using apt as described [here](https://phoenixnap.com/kb/how-to-install-python-3-ubuntu);
3) Install the PAHO MQTT library with the command ```pip3 install paho-mqtt```;
4) Clone this repository;
5) Transfer on multiple Raspberry Pi devices the content of folder NODE_DELIVERY. You should place folder "fs_creato" right under the Desktop folder of the Raspberry taken into account;
6) Enter folder "fs_creato" and type the following two commands: ```sed -i -e 's/\r$//' script2.sh``` and ```chmod +777 ./script2.sh```;
7) Copy on your computer the folder MALWARE_DELIVERY;
8) Type the following two commands: ```sed -i -e 's/\r$//' script.sh``` and ```chmod +777 ./script.sh```;
9) Enjoy!

## Demo Video

[![DEMO](Demo)](https://youtu.be/OfccmiKrc_U) 
