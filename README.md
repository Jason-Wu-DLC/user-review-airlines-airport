Readme

This project will use cloud computing technology to design and implement a big data processing application for analysing airline user feedback. Through in-depth analysis of users' feedback at all stages of boarding, it can help airlines and airport optimize their services and improve users' satisfaction. The customer service quality of airlines and airports directly affects passengers' travel experience. By analysing the data of user comments, airlines and airports can understand the pain points and advantages of user feedback, and then optimize their operations and enhance the competitiveness of airlines.

# Version
Docker latest
Docker-compose 1.26.2
namenode:2.0.0
hadoop3.2.1
resourcemanager:2.0.0
historyserver:2.0.0
hadoop-datanode:2.0.0
spark-worker:3.0.0

# folder
~/infs3208bigdata/             
│
├── docker-compose.yml          
├── hadoop.env                  
├── nbs/                        
│   ├── airline.csv            
│   ├── airport.csv             
│   ├── lounge.csv              
│   └── seat.csv                
│    └── 4 ipynb                
│
├── raw/                        
│   ├── airline.csv            
│   ├── airport.csv             
│   ├── lounge.csv              
│   └── seat.csv                
│
├── volumes/                   
│   ├── hadoop_namenode/        
│   ├── hadoop_datanode1/       
│   ├── hadoop_datanode2/       
│   ├── hadoop_datanode3/       
│   └── hadoop_historyserver/   
│
└── networks/                   
    └── spark-net/              


# Contact
Yulin Wu/
s4565901@student.uq.edu.au


# Setup step
# Update and upgrade the system to ensure all packages are up-to-date
sudo apt update && sudo apt upgrade -y

# Install necessary tools: curl, wget, and git
sudo apt install -y curl wget git

# Install Docker 
sudo apt-get install docker.io -y

# Download and install the specified version of Docker Compose
sudo curl -L "https://github.com/docker/compose/releases/download/1.26.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

# Option 1: Clone the project repository from GitHub
git clone https://github.com/yulin-wu-UQ/infs3208bigdata.git
cd infs3208bigdata

# Option 2: Manually set up the project directory and environment
mkdir ~/infs3208bigdata
cd ~/infs3208bigdata
vim docker-compose.yml  # Create and edit the Docker Compose configuration file
vim hadoop.env  # Create and edit the environment configuration file for Hadoop
mkdir nbs/  # Create a directory for notebook files
mkdir raw/  # Create a directory for raw data files

# Important: Set permissions to ensure Docker can access these directories
sudo chmod -R 777 nbs/
sudo chmod -R 777 raw/

# Start up all containers as defined in the Docker Compose configuration
sudo docker-compose up -d

# Check the status of running Docker containers to ensure they are up and running
sudo docker ps

# Upload data files from the local system to the Hadoop Distributed File System (HDFS)
sudo docker exec -it 0e38cfcfc802 hdfs dfs -put /home/nbs/airline.csv /raw/airline.csv 
sudo docker exec -it 0e38cfcfc802 hdfs dfs -put /home/nbs/airport.csv /raw/airport.csv
sudo docker exec -it 0e38cfcfc802 hdfs dfs -put /home/nbs/lounge.csv /raw/lounge.csv 
sudo docker exec -it 0e38cfcfc802 hdfs dfs -put /home/nbs/seat.csv /raw/seat.csv
