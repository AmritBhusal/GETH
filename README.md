# GETH
GETH setup


Setting up a Private Blockchain:
	In order to set up our own Blockchain network we have first set up a private network which can be given by different nodes but here we have used GETH node to set up a private BLOCKCHAIN Network in a single device. By creating two or more different nodes in different folders we can create a private network in a single device(laptop/pc).

Few steps must be followed to setup private blockchain network
 
Step 1:
	Download and install geth in your device
Required link: https://geth.ethereum.org/downloads/

Step 2:
	Create a folder for a private blockchain network on your device and open it in visual studio and now we will setup the network using terminal.
Firstly we will create two different nodes called node1 and node2
	Command: mkdir node1
		        mkdir node2
Create a password.txt file on both nodes where we will save the password of nodes later.
	
Step 3: 
	Go to node1 using cd node1 
	Create geth within the folder by using command: geth
Create a data directory in node1 using: geth --datadir “./data” account new
Save the password in password.txt file
Let node1 run in the terminal *Repeat the same process for node2 in new terminal

Note: (Note down the password and  node address which  is required in later tasks)















Step 4:
	Let node1 and node2  run in there terminal and open new terminal to create zenesis block
	We use command: puppeth 
	We provide the name to administer. Let be ‘privateblockchain’
	User will get 4 different choices to select 
Show network stats
Configure new genesis
Track new remote server
Deploy network components

	Since we are creating a new genesis block so we will select option 2.

Again user will get two options
Create new genesis from scratch
Import already existing genesis
Since we don't have existing genesis block so we will be creating new genesis block
Choosing option 1
 	Now user will have to choose required consensus from given two option
Ethash - proof-of-work
Clique  - proof-of-authority
	Since we are creating private blockchain so we don't need miners due to which we won't select “Ethash” instead we go by option 2 (Clique)
	
Now we have to decide a time to mine a single block 
For now we take 5 seconds

	One account is needed to seal the network 
(provide the node address of any one of the node)

Select any or all nodes to be pre-funded
(provide node address os all the nodes)

	Now precompile-address should be pre-funded with 1 fei so write yes 

	Now specify network id to make it different and recognisable
	(let us set 12345)

	.json file will be created where we will be initializing our data directory in each node





Step 5: 
	Now we go back to terminal of node1 and we initialize the content of data directory called ‘data’ in .json file 
Using command: geth --datadir ./data init ../privateblockchain.json 
Repeat the process in node2

Step 6: 
	Now we will be creating bootnode
	We will let node1 and node2 run in there terminal and create new terminal to run bootnode
	First we create generation key
	Command to run bootnode: bootnode -genkey bnode.key

	Enter into bootnode using: cd bootnode

	Creating nodekey
	Command used: bootnode -nodekey bnode.key
	We will get enode key which we save for future use

	Now using command: bootnode -nodekey “./bnode.key” -verbosity 7 -addr “127.0.0.1:30301”

Step 7:
	Now to unlock account we will use a geth command
	
	geth --networkid 25734 --datadir “./data” --bootnodes enode://06c7e384aad504783e95a59fc2cd4a6d7f5b1c7acbd9890c2dbe8a0e33cd10c421c650f4ba727de67e64102bb4979ab45d39c48f0bcbef3996b9391016bbe78b@127.0.0.1:0?discport=30301 --port 30303 --ipcdisable --syncmode full --rpc --allow-insecure-unlock --rpccorsdomain “*” --rpcport 8545 --unlock 0x70FE0b4A44c3737818d25437c9C0EF148Ed94063 --password password.txt --mine console

Here the network id is kept from step 4 encode key is kept from step 6 and password.txt is kept from step 2.
Repeat the process for node2 by changing rpc port to 8546


Finally your private blockchain network will be created.
