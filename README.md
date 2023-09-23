# Persist-data-between-two-MySQL-database-hosted-on-two-different-Ec2-instances-using-EBS
What we are going to make:

<img width="740" alt="what-we-going-to-make" src="https://github.com/nobelrakib/Persist-data-between-two-MySQL-database-hosted-on-two-different-Ec2-instances-using-EBS/assets/53372696/eb103345-84ba-4d9d-bbca-e654249512df">

At first launch two ec2 instances and attach a 20 GB EBS volume on instance1.

<img width="762" alt="vmlist" src="https://github.com/nobelrakib/Persist-data-between-two-MySQL-database-hosted-on-two-different-Ec2-instances-using-EBS/assets/53372696/055976a4-2755-4aaa-b73d-c5ef3e8117dc">

<img width="605" alt="20-gb-ebs-volumn" src="https://github.com/nobelrakib/Persist-data-between-two-MySQL-database-hosted-on-two-different-Ec2-instances-using-EBS/assets/53372696/4111037b-5a87-4842-ad90-72b689c83baf">

Now check in instance one list of block using lsblk

<img width="421" alt="vm1detatchblock" src="https://github.com/nobelrakib/Persist-data-between-two-MySQL-database-hosted-on-two-different-Ec2-instances-using-EBS/assets/53372696/90437ce2-15c0-4f99-badd-1231ac8ad546">

See a twenty GB storage has been attached named xvdb.

Now there is no file system in this block storage.

Make a file system.







