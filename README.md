# XLON-nodes-installation
This section is dedicated to the installation procedure of XLON Chain Nodes. Here you will find all the information needed to install and run a node on the Mainnet XLON Chain. In case you face any problems you can always contact us at info@excelon.io

The installation process below will create an Excelon (XLON) Node with RPC access for wallet applications.


Follow the next steps. In any case you can request support at support@excelon.io. We will be happy to help you.


# 1)	Chose your target platform

You can chose any target platform to setup and run your Excelon Node. Windows, Linux, Mac are all appropriate for this task. You only need to keep in mind that certain hardware prerequisites should be in place at the target machine.

For an Ubuntu Linux installation you can chose a machine configuration from well known providers (Digital Ocean, AWS, Azure, etc). Indicatively the instance below would be more than enough to run the Excelon Node:

    •	Ubuntu version: 20.04
    •	Memory: 8 GB 
    •	vCPUs: 4 AMD 
    •	Disk: 160 GB SSD




# 2)	Prepare your network settings for the node

For your Excelon Node, you should allow the following ports and protocols to function properly:

Incoming from any Source 
------------------------------------------
    (SSH)	TCP	Port: 22 
    (RPC)	TCP	Port: 8545 
    (P2P)	TCP	Port: 30300 
    (P2P)	TCP	Port: 30303
    (P2P)	UDP	Port: 30300
    (P2P)	UDP	Port: 30303

Outgoing to any Destination
------------------------------------------
    ICMP	Open to all IPV4 and IPV6
    TCP	Open to all IPV4 and IPV6
    UDP	Open to all IPV4 and IPV6



# 3)	OPENETHEREUM based node installation.
You can lookup openethereum github url for further information at https://openethereum.github.io 


2.1 Once you have setup your machine and you have console access with proper permissions, create a folder with name “excelon” under the /root folder.

2.2 Download the Openethereum release

Go to the Openethereum releases (https://github.com/openethereum/openethereum/releases) and download the version for your platform in the folder “excelon" you have prepared earlier.

Unzip it in the same folder

2.3 Download the excelon.json (Genesis file) and the publicnode.toml (node configuration file) in the same folder “excelon" you have prepared before. You can fnd these files here: https://github.com/excelon-io/XLON-nodes-installation/tree/main/Mainnet/for%20openethereum%20installation

If you have followed the folder configuration as discussed earler (/root/excelon) then you should be ready to run the node. If not, you should edit the paths at the publicnode.toml which point to the Path and the toml file.



2.4 Run the node

By executing the following commands you can start the node

    •	Windows: 	openethereum.exe  --config=excelon
    •	Linux:	    ./openethereum --config=excelon
    •	Mac:	    openethereum --config=excelon


Make sure your node is running and synchronizing by monitoring the console output of the openethereum



# 2.6	Create a service 

In order to assure that your Node will always be up and running, even after restarts, you will need to create a service to auto start the Node.

For Ubuntu Linux you should create a file “excelon.service” under the /etc/systemd/system folder with the following content. Be carefull this content is indicative. 

    [Unit] 
    Description=Excelon Node 
    After=network.target 

    [Service] 
    User=root 
    Group=root 
    ExecStart=/root/excelon/openethereum --config=/root/excelon/node.toml (openthereum, excelon.json,node.toml PATH) 
    Restart=always 

    KillSignal=SIGHUP 

    [Install] 
    WantedBy=default.target


You should then register the service by running:

systemctl enable excelon.service


You can start, stop, get status and restart the service with the following commands:
    • service excelon start
    • service excelon stop/status/restart
    • service excelon status/restart
    • service excelon restart


You can also monitor the activity of the journal by typing the command:

    journalctl -u excelon.service -f




