
# Airline Feedback Analytics Platform

## Project Overview

This project leverages cloud computing technologies to design and implement a big data processing application for analyzing airline customer feedback. The system performs in-depth analysis of passenger feedback across all boarding stages, enabling airlines and airports to:

- Optimize service offerings
- Enhance customer satisfaction metrics
- Identify operational pain points and competitive advantages
- Improve overall travel experience quality

## Technical Specifications

### System Requirements

| Component         | Version           |
|-------------------|-------------------|
| Docker            | Latest            |
| Docker-compose    | 1.26.2            |
| Hadoop Namenode   | 2.0.0             |
| Hadoop Core       | 3.2.1             |
| Resource Manager  | 2.0.0             |
| History Server    | 2.0.0             |
| Hadoop Datanode   | 2.0.0             |
| Spark Worker      | 3.0.0             |

### Repository Structure

```
infs3208bigdata/
├── docker-compose.yml          # Container orchestration configuration
├── hadoop.env                  # Hadoop environment variables
├── nbs/                        # Jupyter notebooks and processed data
│   ├── airline.csv            
│   ├── airport.csv             
│   ├── lounge.csv              
│   ├── seat.csv                
│   └── *.ipynb                 # Analysis notebooks
│
├── raw/                        # Raw data sources
│   ├── airline.csv            
│   ├── airport.csv             
│   ├── lounge.csv              
│   └── seat.csv                
│
├── volumes/                    # Persistent data storage
│   ├── hadoop_namenode/        
│   ├── hadoop_datanode1/       
│   ├── hadoop_datanode2/       
│   ├── hadoop_datanode3/       
│   └── hadoop_historyserver/   
│
└── networks/                   # Docker networking
    └── spark-net/              
```

## Deployment Guide

### Prerequisites

1. Update system packages:
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```

2. Install required utilities:
   ```bash
   sudo apt install -y curl wget git
   ```

### Docker Installation

1. Install Docker Engine:
   ```bash
   sudo apt-get install docker.io -y
   ```

2. Install Docker Compose:
   ```bash
   sudo curl -L "https://github.com/docker/compose/releases/download/1.26.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
   sudo chmod +x /usr/local/bin/docker-compose
   ```

### Project Setup

**Option 1: Clone Repository**
```bash
git clone (https://github.com/Jason-Wu-DLC/user-review-airlines-airport/)
```

**Option 2: Manual Setup**
```bash
vim docker-compose.yml  # Configure container services
vim hadoop.env         # Set Hadoop environment variables
mkdir nbs/ raw/       # Create data directories
```

### Permissions Configuration
```bash
sudo chmod -R 777 nbs/
sudo chmod -R 777 raw/
```

### Service Initialization
```bash
sudo docker-compose up -d
```

### Verification
```bash
sudo docker ps  # Verify container status
```

### Data Ingestion
```bash
# Upload datasets to HDFS
sudo docker exec -it <container_id> hdfs dfs -put /home/nbs/airline.csv /raw/airline.csv
sudo docker exec -it <container_id> hdfs dfs -put /home/nbs/airport.csv /raw/airport.csv
sudo docker exec -it <container_id> hdfs dfs -put /home/nbs/lounge.csv /raw/lounge.csv
sudo docker exec -it <container_id> hdfs dfs -put /home/nbs/seat.csv /raw/seat.csv
```

## Support & Contact

**Maintainer:** Yulin Wu  
**Email:** [jasonwu940@outlook.com](mailto:jasonwu940@outlook.com)
```

Key improvements made:
1. Added clear section headers and logical organization
2. Implemented tables for version information
3. Formatted code blocks with proper syntax highlighting
4. Improved directory tree visualization
5. Structured deployment steps in a numbered sequence
6. Added proper Markdown formatting for commands and paths
7. Included email link formatting
8. Maintained all original technical content while enhancing readability
9. Added consistent spacing and section separation
