# GCP Data Fusion Private IP with Peering VPC
- Make Data Fusion can access proxysql in private network/ip, you no need make proxysql / haproxy with public network/ip
- VPC Peering  = vpc-datafusion <--peered--> vpc-production
- Topology Connection = data fusion --> vm proxysql/haproxy ---> cloudsql
- Create IAM user for data fusion
- Create firewall rules for dataproc VM-to-VM communication
- Data Fusion until now can't access direct to private ip CloudSQL so you need create proxysql or haproxy in private network


## Create Data Fusion Instance with Private IP and use our VPC Production

![alt text](https://i.imgur.com/zXArtrw.png)

## Create VPC Peering from network Data Fusion to our production VPC
#### For Project ID and VPC network name. you can get in Data Fusion Dashbaord in Instance Service Account
```
Service Account = cloud-datafusion-management-sa@v15658555zxbe45p-tp.iam.gserviceaccount.com
Instance ID = production-data-fusion
Region = asia-southeast1
```
![alt text](https://i.imgur.com/96tzzVr.png)

#### Try Connect Data Fusion to private vm proxysql
![alt text](https://i.imgur.com/zTmXtrE.png)
![alt text](https://i.imgur.com/tCqHyCK.png)
![alt text](https://i.imgur.com/rkQQfLd.png)



## Config iam user for data fusion
#### Create iam user for make data fusion instance have access to dataproc,bigquery etc in our project
- copy service account in instance data fusion example Service Account = cloud-datafusion-management-sa@v15658555zxbe45p-tp.iam.gserviceaccount.com
- create new iam user in our project with Role = 
```
Cloud Data Fusion API Service Agent
Service Account User
```
![alt text](https://i.imgur.com/Z6M2lqY.png)


## Config firewall internal IP VM-to-VM communication for Dataproc
![alt text](https://i.imgur.com/2NPFb1e.png)
![alt text](https://i.imgur.com/ALtFrbg.png)
