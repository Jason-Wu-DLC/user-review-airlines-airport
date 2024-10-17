Readme

This project will use cloud computing technology to design and implement a big data processing application for analysing airline user feedback. Through in-depth analysis of users' feedback at all stages of boarding, it can help airlines and airport optimize their services and improve users' satisfaction. The customer service quality of airlines and airports directly affects passengers' travel experience. By analysing the data of user comments, airlines and airports can understand the pain points and advantages of user feedback, and then optimize their operations and enhance the competitiveness of airlines.

Version
Docker latest
Docker-compose 1.26.2
namenode:2.0.0
hadoop3.2.1
resourcemanager:2.0.0
historyserver:2.0.0
hadoop-datanode:2.0.0
spark-worker:3.0.0

folder
~/infs3208bigdata/             
│
├── docker-compose.yml          # Docker Compose configuration file │
├── hadoop.env                  # Environment variable file for Hadoop and Spark configuration│
├── nbs/                        # Directory for storing Jupyter Notebook files and code
│   ├── airline.csv             # Dataset file for airlines
│   ├── airport.csv             # Dataset file for airports 
│   ├── lounge.csv              # Dataset file for lounges 
│   └── seat.csv                # Dataset file for seats
│    └── 4 ipynb                # jupyter notebook code
│
├── raw/                        # Directory for raw data files, typically uploaded to HDFS 
│   ├── airline.csv             # Same airline dataset in raw format 
│   ├── airport.csv             # Same airport dataset in raw format 
│   ├── lounge.csv              # Same lounge dataset in raw format
│   └── seat.csv                # Same seat dataset in raw format 
│
├── volumes/                    # Volumes for Hadoop data nodes, NameNode, and history server 
│   ├── hadoop_namenode/        # Volume for Hadoop NameNode 
│   ├── hadoop_datanode1/       # Volume for Hadoop DataNode 1 
│   ├── hadoop_datanode2/       # Volume for Hadoop DataNode 2 
│   ├── hadoop_datanode3/       # Volume for Hadoop DataNode 3
│   └── hadoop_historyserver/   # Volume for Hadoop History Server 
│
└── networks/                   # Docker network configuration for container communication 
    └── spark-net/              # Custom bridge network for Spark and Hadoop containers 


Contact
Yulin Wu
s4565901@student.uq.edu.au


Setup step
# Update and upgrade the system packages to the latest versions
sudo apt update && sudo apt upgrade -y 

# Install essential utilities like curl, wget, and git
sudo apt install -y curl wget git

# Create a project directory and navigate into it
mkdir ~/infs3208bigdata
cd ~/infs3208bigdata

# Install Docker to manage containers
sudo apt-get install docker.io -y

# Download the specified version of Docker Compose and make it executable
sudo curl -L "https://github.com/docker/compose/releases/download/1.26.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

# Create and open a new Docker Compose YAML configuration file (Copy file)
vim docker-compose.yml

# Create and open an environment variable file for Hadoop and Spark configurations
vim hadoop.env

# Create directories for Jupyter notebooks and raw data
mkdir nbs/
mkdir raw/

# Set read, write, and execute permissions for all users on these directories
sudo chmod -R 777 nbs/
sudo chmod -R 777 raw/

# Start the Docker containers in detached mode as defined in the Docker Compose file
sudo docker-compose up -d

# List all running Docker containers to verify that everything is running as expected
sudo docker ps

# Execute commands inside the running Hadoop Namenode container to create a new directory in HDFS
sudo docker exec -it 0e38cfcfc802 hdfs dfs -mkdir -p /raw

# Upload datasets from the Jupyter notebook directory to the HDFS directory created above
sudo docker exec -it 0e38cfcfc802 hdfs dfs -put /home/nbs/airline.csv /raw/airline.csv
sudo docker exec -it 0e38cfcfc802 hdfs dfs -put /home/nbs/airport.csv /raw/airport.csv
sudo docker exec -it 0e38cfcfc802 hdfs dfs -put /home/nbs/lounge.csv /raw/lounge.csv
sudo docker exec -it 0e38cfcfc802 hdfs dfs -put /home/nbs/seat.csv /raw/seat.csv

