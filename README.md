# End-to-End-MERN-Application-Deployment-and-Monitoring-with-Terraform-Ansible-Prometheus-and-Grafana

.env file to work with the backend after creating a database in mongodb:
MONGO_URI='ENTER_YOUR_URL'
PORT=3001

Data format;
{
    "tripName": "Incredible India",
    "startDateOfJourney": "19-03-2022",
    "endDateOfJourney": "27-03-2022",
    "nameOfHotels":"Hotel Namaste, Backpackers Club",
    "placesVisited":"Delhi, Kolkata, Chennai, Mumbai",
    "totalCost": 800000,
    "tripType": "leisure",
    "experience": "Lorem Ipsum, Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum, ",
    "image": "https://t3.ftcdn.net/jpg/03/04/85/26/360_F_304852693_nSOn9KvUgafgvZ6wM0CNaULYUa7xXBkA.jpg",
    "shortDescription":"India is a wonderful country with rich culture and good people.",
    "featured": true
}



REACT_APP_BACKEND_URL=http://localhost:3001 
<img width="495" height="592" alt="image" src="https://github.com/user-attachments/assets/2a51e338-09f3-4419-b007-b7087fc63088" />

Title: End-to-End MERN Application Deployment and Monitoring

1. Introduction
   - Objective: Deploy and monitor a MERN app using Terraform, Ansible, Prometheus, and Grafana.

2. Infrastructure Provisioning (Terraform)
   - AWS Provider setup
   - EC2 instances for web and DB
   - Security groups and IAM roles
   - Outputs: Public IPs of instances

3. Configuration Management (Ansible)
   - Inventory setup with EC2 IPs
   - Web server: Node.js, NPM, app clone, .env config
   - DB server: MongoDB install, DB/user creation, remote access
   - Security: SSH hardening, firewall rules

4. Monitoring Setup
   - Prometheus: Installed on web server, Node.js metrics via prom-client
   - MongoDB Exporter: Installed on DB server
   - Grafana: Dashboards for backend, DB, frontend metrics
   - Alerts: Error rate, slow API, MongoDB issues

5. Architecture Diagram
   - [Insert diagram showing EC2 instances, Prometheus, Grafana, MongoDB]

6. Performance Analysis
   - Backend latency: Avg 120ms
   - MongoDB ops/sec: ~300
   - Error rate: <1%

7. Issues Faced
   - SSH key mismatch: Resolved by regenerating keys
   - MongoDB remote access: Fixed by binding to 0.0.0.0 and updating firewall

8. Conclusion
   - Successfully deployed and monitored a production-grade MERN app
   - Infrastructure is reproducible and observable

[Web Server] <---> [MongoDB Server]
     |                   |
[Prometheus]         [MongoDB Exporter]
     |
[Grafana Dashboards]

Part 1: Infrastructure Provisioning with Terraform
1. AWS Setup:
○ Configure AWS CLI with credentials
○ Initialize Terraform and define AWS as the provider
2. Networking Configuration:
○ Use Default VPC
○ Attach an Internet Gateway
○ Configure a Route Table to enable internet access
3. EC2 Instances:

○ Provision two EC2 instances:
■ One for the MERN web server
■ One for the MongoDB database
○ Both instances should be placed in the same public subnet
○ Generate Terraform outputs.tf to display the public IPs

4. Security Groups:
○ Web server: Allow inbound HTTP/HTTPS/SSH
○ DB server: Allow SSH and only allow MongoDB port (27017) from the web
server’s security group  
5. IAM Roles:      ○ Create IAM roles for monitoring and log access (if needed for Prometheus,
CloudWatch, etc.)



Part 2: Configuration Management with Ansible
1. Inventory Setup:
○ Use public IPs of EC2 instances in the Ansible inventory file
2. Web Server (App Server) Setup:
○ Install Node.js and NPM
○ Clone the TravelMemory app repo
○ Install backend and frontend dependencies
○ Configure .env variables
○ Start the Node.js backend and React frontend
3. Database Server Setup:
○ Install and configure MongoDB
○ Create application DB and users
○ Enable remote access with firewall restrictions
4. Security Configuration:
○ Harden SSH access (disable root login, use SSH key pairs)
○ Apply firewall rules using ufw or security groups


Part 3: Observability and Monitoring Setup
1. Prometheus:
○ Install Prometheus on the web server using Ansible
○ Use prom-client in Node.js backend to expose:
■ API latency
■ Error rate
■ Request count
○ Install MongoDB Exporter on the DB instance to collect DB metrics
2. Grafana Dashboards:
○ Install Grafana on the web server
○ Create dashboards to visualize:
■ Custom backend metrics
■ MongoDB performance
■ Frontend response metrics (optional)
3. Alerting & Anomaly Detection:
○ Set alert rules in Grafana for:

■ High error rates
■ MongoDB performance issues
■ Slow API responses
○ Enable basic anomaly detection using Prometheus data
Part 4: Documentation & Reporting
● Provide full documentation:
○ Terraform and Ansible setup
○ Application architecture (diagram)
○ Metric and log configuration
○ Grafana dashboards and alert rules (screenshots)
● Include performance analysis using collected metrics


Deliverables:
● GitHub repository containing:
○ Terraform code (terraform/)
○ Ansible playbooks (ansible/)
○ Prometheus and Grafana configuration (monitoring/)
○ Documentation (docs/README.md or PDF)
● Include:            
○ Terraform outputs
○ Sample .env file (with secrets redacted)
○ Screenshots of Grafana dashboards and alert configuration
