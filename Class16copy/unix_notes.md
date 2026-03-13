## Core Unix commands

Most unix commands have super short names, which make them quick to 
type but annoying to learn. Major file system related commands include: 

pwd: Print working directory 
ls: List files and directories
cd: Change directory
mkdir: Make a new directory
rm: Remove files and directories (delete)zh
cp: Copy files (source > destination) 
mv: Move files or dirs (basically re-name)
nano: A wee text editor (very basic but always available) 
curl: Download files from web
wget: DOwnload files from the web
tar -zxvf: untar (unpackage) Tr archive files
gunzip: UnZip files
$PATH: The places (dirs) to look for programs.

## AWS EC2 Instance

Connect to my instance with: 

ssh -i ~/Downloads/bimm143_eric.pem ubuntu@ec2-54-213-147-54.us-west-2.compute.amazonaws.com

Secure Copy files between machines, in this case from our instance to our laptop

ssh -i ~/Downloads/bimm143_eric.pem ubuntu@ec2-54-213-147-54.us-west-2.compute.amazonaws.com:/home/ubuntu/work/bimm143_github/Class16/results.txt 



## Class 17 instance
ssh -i ~/Downloads/bimm143_eric.pem ubuntu@ec2-35-86-136-184.us-west-2.compute.amazonaws.com

export KEY = ~/Downloads/bimm143_eric.pem

export SERVER=ubuntu@ec2-35-86-136-184.us-west-2.compute.amazonaws.com

ssh -i $KEY $SERVER


