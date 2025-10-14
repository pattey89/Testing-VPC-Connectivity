<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Testing VPC Connectivity

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-connectivity)

**Author:** PATRICK ADDAI  
**Email:** patrickaddai1689@gmail.com

---

## Testing VPC Connectivity

![Image](http://learn.nextwork.org/refreshed_amber_shy_cantaloupe/uploads/aws-networks-connectivity_8ee57662)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon Virtual Private Cloud (VPC) allows users to create a logically isolated section within the AWS cloud, enabling them to define their own virtual network, similar to a traditional on-premises network, but with the scalability and flexibility of AWS. It provides enhanced security, control over network configuration, and seamless integration with other AWS services. 



### How I used Amazon VPC in this project

In today's project, we used Amazon VPC to set up a VPC and its components using the VPC wizards, and then launched EC2 instances AND tested the connectivity between my network resources.

### One thing I didn't expect in this project was...

I didn't expect for a network ACL's Source to point to an incorrect subnet CIDR block. This was a great reminder of the importance to slowing down and double checking configuration settings when using the VPC wizard to automate and creating the VPC.

### This project took me...

This project took me 2 hours 45 minutes, including demo time and troubleshooting.

---

## Connecting to an EC2 Instance

Connectivity is all about how well different parts of your network talk to each other and with external networks. It's essential because connectivity is how data flows smoothly across your network, powering everything from simple web hosting on the Internet to complex operations e.g. Netflix using over 100,000 EC2 instances to power its streaming platform. Solid connectivity is the backbone of any system that relies on network interactions, making every communication and operation reliable and efficient.

My first connectivity test was whether I could connect to my NextWork Public Server (an EC2 instance).

![Image](http://learn.nextwork.org/refreshed_amber_shy_cantaloupe/uploads/aws-networks-connectivity_88727bef)

---

## EC2 Instance Connect

I connected to my EC2 instance using EC2 Instance Connect, which is an alternative way to use SSH - Instance Connect that lets you securely connect to your EC2 instances directly using the AWS Management Console.

My first attempt at getting direct access to my public server resulted in an error, because the security group associated with NextWork Public Server lets in all inbound HTTP traffic, instead of using SSH through EC2 Instance Connect.

I fixed this error by updating NextWork Public Server's security group so it can let in SSH traffic. Choosing Anywhere-IPv4 as the source lets in SSH connections from any IPv4 address.

![Image](http://learn.nextwork.org/refreshed_amber_shy_cantaloupe/uploads/aws-networks-connectivity_1cbb1b88)

---

## Connectivity Between Servers

Ping is a common computer network tool used to check whether your computer can communicate with another computer or device on a network. I used ping to test the connectivity between my Nextwork Public Server and Private Server.

The ping command I ran was Ping followed by Nextwork Private IPV4 address of my private server.

The first ping returned only No replies from the private server. This meant security settings with my private server was blocking inbound (and or outbound) ICMP traffic, which is the traffic type of ping messages.

![Image](http://learn.nextwork.org/refreshed_amber_shy_cantaloupe/uploads/aws-networks-connectivity_defghijk)

---

## Troubleshooting Connectivity

'I troubleshooted this by enabling ICMP traffic in my private server's network ACLs and security groups. I also made sure the Source I defined in my network ACL correctly pointed to my Public Subnet.

![Image](http://learn.nextwork.org/refreshed_amber_shy_cantaloupe/uploads/aws-networks-connectivity_4a9e8014)

---

## Connectivity to the Internet

curl is a tool to test connectivity in a network. Where ping checks if one computer can contact another (and how long messages take to travel back and forwth), curl is used to transfer data to or from a server. That means on top of checking connectivity, you can use curl to grab data from, or upload data into other servers on the internet!

I used curl to test the connectivity between my network's Public Server with the Public internet! This test would only be successful if my internet gateway, network ACLs, security groupds and route tables were set up correctly.

### Ping vs Curl

Ping and curl are different because they return different responses to my Public Server's terminal - ping responds with a report on the performance of connectivity with my Private Server whiles curl responded with HTML data from another public server.

---

## Connectivity to the Internet

I ran the curl command curl https://learn.nextwork.org/projects/aws-host-a-website-on-s3 which returned the HTML content of Nextwork's first project guide.

![Image](http://learn.nextwork.org/refreshed_amber_shy_cantaloupe/uploads/aws-networks-connectivity_8ee57662)

---

---
