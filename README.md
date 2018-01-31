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



