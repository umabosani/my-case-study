# my-case-study

aws ec2 create-key-pair --key-name casestudy-key

##  added a rule that allows incoming traffic over port 22 for SSH

aws ec2 authorize-security-group-ingress --group-name Casestudy-sg --protocol tcp --port 22 --cidr 172.31.0.0/20

## describe the security group-id
aws ec2 describe-security-groups --group-id sg-1c87516baws ec2 describe-security-groups --group-id sg-1ca15b6b
{
    "SecurityGroups": [
        {
            "IpPermissionsEgress": [
                {
                    "IpProtocol": "-1",
                    "PrefixListIds": [],
                    "IpRanges": [
                        {
                            "CidrIp": "0.0.0.0/0"
                        }
                    ],
                    "UserIdGroupPairs": [],
                    "Ipv6Ranges": []
                }
            ],
            "Description": "Mywebdmz",
            "IpPermissions": [
                {
                    "PrefixListIds": [],
                    "FromPort": 80,
                    "IpRanges": [
                        {
                            "CidrIp": "49.36.1.193/32"
                        }
                    ],
                    "ToPort": 80,
                    "IpProtocol": "tcp",
                    "UserIdGroupPairs": [],
                    "Ipv6Ranges": []
                }
            ],
            "GroupName": "Mywebdmz",
            "VpcId": "vpc-12e4ed6a",
            "OwnerId": "929628204957",
            "GroupId": "sg-1ca15b6b"
        }
    ]
}

## Creating Ec2 instance

aws ec2 run-instances --image-id ami-0a9fac70 --security-group-ids sg-1c87516b --count 1 --instance-type t2.micro --key-name casestudy-key


Why I have choosen Ubuntu: Justification:

Docker for Ubuntu is the best way to install the Docker platform on Ubuntu Linux environments. Simplify provisioning and setup of Docker and accelerate your time to value in building and deploying container based applications.
Even it is suitable openresty Web Server. Ubunu easy to manage and it supports for Docker and Openresty.

Docker for Ubuntu is available for free Community Edition (CE) and as an Enterprise Edition (EE) subscription with software, support and certification.

These are the reasons that I have to Ubuntu.





Openresty git clone:

 sudo git clone https://github.com/openresty/openresty


Configuration Management using chef:


## Here in this script few things could be assumptions.

#create Chef-repo directory on my work station:

cd ~/chef-repo

# create the chef cookbook on openresty:

knife cookbook create openresty

package 'nginx' do
  action :install
end

service 'nginx' do
  action [ :enable, :start ]
end

## We should put this file in the files/default sub directory

cd ~/chef-repo/cookbooks/nginx/files/default

## edit the index.html file

<html>
  <head>
    <title>Cognative Scale</title>
  </head>
  <body>
    <h1>test website</h1>
    <p>casestudy</p>
  </body>
</html>

## to update the node need to create the cookbook "sudo apt-get update"

knife cookbook create aptupdate

## we need to edit the default recipy on our cookbook
nano ~/chef-repo/cookbooks/apt/recipes/default.rb

execute "apt-get update" do
  command "apt-get update"
end

## update our openrecipy cookbook.

nano ~/chef-repo/cookbooks/nginx/recipes/default.rb

include_recipe "apt"

package 'nginx' do
  action :install
end

service 'nginx' do
  action [ :enable, :start ]
end

cookbook_file "/usr/share/nginx/www/index.html" do
  source "index.html"
  mode "0644"
end

## Update the metadata.rb file

nano ~/chef-repo/cookbooks/nginx/metadata.rb

name,
Maintainer_email
license
description
version

depends on aptupdate


## Upload the cookbooks to our server

knife cookbook upload aptupdate
knife cookbook upload nginx

## modify the run list of our node

knife node edit nginx

## node list

knife node list

## edit the node
knife node edit chefclient1

{
  "name": "client1",
  "chef_environment": "_default",
  "normal": {
    "tags": [

    ]
  },
  "run_list": [
    "recipe[openresty]"
  ]
}

## ssh into node

sudo chef-client

test the resources


## Based on the assumptions i have written the code for openresty web server. Kindly let me know if you need detail information on this.

Dockerize the application:

# check for kernal version.
uname -r

# installing the docker

sudo curl -sSL https://get.docker.com/ | sh

#testing after installation.

sudo docker run hello-world

sudo docker ps -a

sudo docker ps -a


sudo docker start pedantic_snyder


# pulling the nginx docker image

sudo docker pull nginx

sudo docker run --name docker-nginx -p 80:80 nginx

sudo docker ps -a

sudo docker rm docker-nginx

sudo docker run --name docker-nginx -p 80:80 -d nginx
sudo docker ps

sudo docker stop docker-nginx

sudo docker rm docker-nginx

# building a webpage

mkdir -p ~/docker-nginx/html
cd ~/docker-nginx/html

vim index.html

<html>
  <head>
    <title>Cognitive_Scale</title>
  </head>
  <body>
    <h1>Casestudy</h1>
    <p>DevOps</p>
  </body>
</html>

sudo docker run --name docker-nginx -p 80:80 -d -v ~/docker-nginx/html:/usr/share/nginx/html nginx


cd ~/docker-nginx

sudo docker cp docker-nginx:/etc/nginx/conf.d/default.conf default.conf

sudo docker stop docker-nginx

sudo docker rm docker-nginx

sudo docker run --name docker-nginx -p 80:80 -v ~/docker-nginx/html:/usr/share/nginx/html -v ~/docker-nginx/default.conf:/etc/nginx/conf.d/default.conf -d nginx

sudo docker restart docker-nginx



## Restricting security groups to  the access application from my ip.

I can update the security group inbound rules for this application. 

type: http
protocol: tcp
port range: 80
## source: myip/32 ( 49.36.3.258/32)

for the email alert notication with the free software solutions. ( There are multiple paid services are available on website monitoring).

I used one of the google provide alert notification and have shared with the devops@cognitivescale.com

and I also got a reply from them.


jtischler@cognitivescale.com is requesting access to the following spreadsheet:

Copy of Website Monitor v5.0 by ctrlq.org
Open sharing settings
Google Sheets: Create and edit spreadsheets online. 
Google Inc. 1600 Amphitheatre Parkway, Mountain View, CA 94043, USA
You have received this email because someone shared a spreadsheet with you from Google Sheets.


## Kindly note based on my busy schedule I could work on this case study this much only. 

Kindly let me know if you need more information on this. But I am really sorry to say, I am too much busy with preparation and other interview schedules.
