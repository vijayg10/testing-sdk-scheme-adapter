# AWS Deployment with Letsencrypt SSL certificates

## Launch an EC2 instance in AWS console

* Create an EC2 instance in AWS console and select **t2.micro** instance type.
* Select **Ubuntu 18.04** as your operating system.
* After your instance is ready, you can connect to it using ssh and the downloaded key file from AWS EC2 dashboard.
* Install docker and docker-compose in that EC2 instance

## Open 4000 TCP port in security groups and assign elastic IP

* Add the inbound rule in security group of this EC2 instance that will expose the TCP 4000 port to public
* Use Elastic IP service to assign a static IP for this instance

## Setup domain name for this instance

* You can use route53 in aws or any other DNS service to point a DNS name to this IP address
* This step is required because the Let's Encrypt certificate authority will not issue certificates for a bare IP address.
  
## Get SSL certificate from Let's Encrypt

* You can get SSL certificate for the above domain name from any of the certification authority, where as this step is for Let's encrypt because its free.
* The easiest way to get SSL from Let's encrypt is as follows
  * Install Nginx in the EC2 instance
  * You can follow this [link](https://certbot.eff.org/lets-encrypt/ubuntubionic-nginx) to install certbot and get the ssl certificates.
  * Your certificates will be in the folder /etc/letsencrypt/live/<your_domain_name>
  * You can use these certificates in the scheme adapter repo as follows. Please refer scheme adapter environment file.
    * chain.pem -> IN_CA_CERT_PATH
    * cert.pem -> IN_SERVER_CERT_PATH
    * privkey.pem -> IN_SERVER_KEY_PATH

## 