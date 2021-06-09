# Valaxy Assignment1

![Screenshot (134)](https://user-images.githubusercontent.com/28533352/120897550-6933a480-c644-11eb-9d37-9f555938acef.png)

Please create private EC2 instance with "t2.micro" type in AWS cloud and the required dependency resources to connect to the private EC2 server as per the architecture shown above.

# Solution


#### Cloudformation Stack
Total 5 stacks

1. vpc.yaml
2. SecurityGroupInPublic.yaml
3. SecurityGroupInPrivate.yaml
4. Ec2InPublic.yaml
5. Ec2InPrivate.yaml

### 1. VPC.yaml

This stack will create 
- **VPC** 
- **Public Subnet** 
- **Private Subnet** 
- **Internet Gateway** 
- **Public Route Table** 
- **Private Route Table** 
- **Route Table Association to subnets** 

#####  Input Parameters for the stack

By Default it will take this Input(Change accordingly)
![Screenshot (135)](https://user-images.githubusercontent.com/28533352/120898014-c16ba600-c646-11eb-8e88-b149e58b552b.png)

##### Created Resources  
![Screenshot (136)](https://user-images.githubusercontent.com/28533352/120898308-f5939680-c647-11eb-9211-f096bed6601f.png)

##### Outputs
![Screenshot (137)](https://user-images.githubusercontent.com/28533352/120898385-4b683e80-c648-11eb-9443-b135d5446c27.png)

---

### 2.SecurityGroupInPublic.yaml
This stack will create 
- **Security Group** 
Security Group for Instances in **Public Subnet** 

Which allows **SSH** from Public Internet

#####  Input Parameters for the stack 
By Default it will take this Input(Change accordingly)
![Screenshot (138)](https://user-images.githubusercontent.com/28533352/120898776-093ffc80-c64a-11eb-80f0-bce1535e6a90.png)

#####  Created Resources 
![Screenshot (140)](https://user-images.githubusercontent.com/28533352/120898791-27a5f800-c64a-11eb-9f6b-e383615af998.png)

#####  Outputs 
![Screenshot (140)](https://user-images.githubusercontent.com/28533352/120898821-4ad0a780-c64a-11eb-8460-67b299b13643.png)

---

### 3.SecurityGroupInPrivate.yaml
This stack will create 
- **Security Group** 
Security Group for Instances in **Private Subnet**

Which allows **SSH** only from Public Subnet Instance

#####  Input Parameters for the stack 
By Default it will take this Input(Change accordingly)
![Screenshot (142)](https://user-images.githubusercontent.com/28533352/120899010-2a551d00-c64b-11eb-95ab-f65aac05e6c5.png)

#####  Created Resources 
![Screenshot (142)](https://user-images.githubusercontent.com/28533352/120899021-3b059300-c64b-11eb-943e-e8c34cd30d1c.png)

##### Outputs
![Screenshot (143)](https://user-images.githubusercontent.com/28533352/120899029-48228200-c64b-11eb-8a76-a02bb38ceff4.png)

---

### 4. Ec2InPublic.yaml
This stack will create 
- **EC2 Instance**
VolumeSize: 8 
VolumeType: gp2  
KeyPair(Select the existing keypair)
Pubic Ip
PublicDNS Name
Private IP
PrivateDNS Name
Security Group(Created using 2nd stack)

#####  Input Parameters for the stack 
By Default it will take this Input(Change accordingly)
![Screenshot (144)](https://user-images.githubusercontent.com/28533352/120899240-51f8b500-c64c-11eb-836a-7e843c093a1c.png)

#####  Created Resources 
![Screenshot (145)](https://user-images.githubusercontent.com/28533352/120899254-66d54880-c64c-11eb-98d2-e06eca0567fc.png)

##### Outputs 
![Screenshot (146)](https://user-images.githubusercontent.com/28533352/120899271-7d7b9f80-c64c-11eb-8b90-c953d5422b3d.png)

---

### 5. Ec2InPrivate.yaml
This stack will create 
- **EC2 Instance**
VolumeSize: 8 
VolumeType: gp2  
KeyPair(Select the existing keypair)
Private IP
PrivateDNS Name
SecurityGroup(created using 3rd stack)

##### Input Parameters for the stack 
By Default it will take this Input(Change accordingly)
![Screenshot (148)](https://user-images.githubusercontent.com/28533352/120899340-e236fa00-c64c-11eb-90bd-990eb23b234b.png)

##### Created Resources 
![Screenshot (149)](https://user-images.githubusercontent.com/28533352/120899362-01358c00-c64d-11eb-9806-3de9b11ffcc3.png)

#####  Outputs 
![Screenshot (150)](https://user-images.githubusercontent.com/28533352/120899387-1ad6d380-c64d-11eb-91a9-ca245b3eb4fd.png)

---

# Cloudformation Exports

![Screenshot (151)](https://user-images.githubusercontent.com/28533352/120899498-a6e8fb00-c64d-11eb-871d-971704340b15.png)

![Screenshot (152)](https://user-images.githubusercontent.com/28533352/120899508-b23c2680-c64d-11eb-8cec-87cb8e0247f3.png)

![Screenshot (153)](https://user-images.githubusercontent.com/28533352/120899523-c08a4280-c64d-11eb-9b64-00e788b85a48.png)

---

## Things to do After Stack Creation

1.**SSH** into public Subnet
2.Download KeyPair in **EC2**
3.Change the permission of the **keypair**
 ```
 sudo su
 chmod 0400 keypairname.pem
 ```

4. **SSH** into public Subnet
From **Public** instance **SSH** to the **Private** instance 

 ```
 ssh ecc2-user@privateIP -i keyname.pem
 ```

 ![Screenshot (154)](https://user-images.githubusercontent.com/28533352/120899889-89b52c00-c64f-11eb-9d23-6ac3b3fc4656.png)
