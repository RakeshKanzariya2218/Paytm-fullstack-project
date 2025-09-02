# paytm Project

This repository contains both backend and frontend code for the Paytm project.

## Structure

- **Backend/**
  - `rds.py`: Backend logic for RDS operations.
- **Frontend/**
  - **Frontend-code/**: Contains HTML and CSS files for the main web interface.
    - `index.html`, `main.html`, `processing.html`, `recharge.html`, `signup.html`, `signuppscanner.html`, `summary.html`: Web pages for different functionalities.
    - `responsive.css`, `style.css`: Stylesheets for responsive and general styling.
  - **Frontend-S3/**: Contains backend code and policy for S3 integration.
    - `backends3.py`: Python backend for S3 operations.
    - `s3backendpolicys.txt`: S3 policy definitions.

## Getting Started
- **Rds/**
1. create Rds in same vpc 
- **Backend-setup/**
- create backend server and add i am role access to the s3 bucket
1. Clone the repository to your backend server.
```
sudo yum install git -y
git clone https://github.com/CloudTechDevOps/Paytm-fullstack-project.git
```
switch to backend
``` 
 cd Paytm-fullstack-project/Backend
```
2. install dependencys 
```
sudo yum update -y
sudo dnf install -y mariadb105
sudo yum install python3 -y
sudo yum install python3-pip -y
python3 --version pip3 --version
```
3. Run the requirements.tx on backend path
```
pip install -r requirements.txt
```
4. change the rds details on **rds.py**
5. create database and tables by using below command
```
mysql -h rds-endpoint -u admin -p<rds-password> < paytm.sql
```
6. Finally run the **rds.py**
```
nohup python3 rds.py > rds.log 2>&1 &
```
- **S3-setup/**
1. Create s3 bucket public or private if you create private you need to add bucket policy to 

- **Frontend-setup/**
- create frontend server and add i am role access to the s3 bucket

1. Clone the repository to your frontend server.
```
sudo yum install git -y
git clone https://github.com/CloudTechDevOps/Paytm-fullstack-project.git
```

2. switch to frontend
``` 
 cd Paytm-fullstack-project/Frontend
 ```
3. siwtch to frontend s3
```
 cd Frontend-S3
 ```
4. install dependencys 
```
sudo yum update -y
sudo yum install python3 -y
sudo yum install python3-pip -y
python3 --version pip3 --version
```
5. Run the requirements.tx on frontend-s3 path
```
pip install -r requirements.txt
```
6. change the s3 bucket name on **backends3.py**  file if you are using private s3 add the bucket policy.Policy is there on **s3backendpolicy.txt**
```
###Bucket policy here change your bucket name and ec2 role and all 
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::accountnumber:role/rolename"
            },
            "Action": "s3:*",
            "Resource": [
                "arn:aws:s3:::bucketname",
                "arn:aws:s3:::bucketname/*"
            ]
        }
    ]
}
```
8. Finally run the **backends3.py**
```
nohup python3 backends3.py > backend.log 2>&1 &
```
8. If you want to create loadbalncer for this s3 just create with 5000 port other wise ignore for pulic deployment

9. switch to frontend-code
```
cd ..
cd Frontend-code
```
10. change the backend url on following files **signup.html** **signuppscannerhtml**  if your are using loadbalncer for backend paste loadbalncer url otherwise paste public ip:5000   like this change any one 
```
// Set your backend API URL here
      const API_URL = "http://backend-1090030115.ap-northeast-1.elb.amazonaws.com";
    //const API_URL = "http://publicip-backend:5000";
``` 
11. then change the s3 url on **summary.html** file either loadbalncer or public:500 port 
```
      // change here frontend-public-ip:5000/upload
      // if ypu are using loadblancer for frontend s3 just paste that url
      fetch("http://s3copy-446514415.ap-northeast-1.elb.amazonaws.com/upload", {
        method: "POST",
        body: formData
      })
```
12. install the dependyces on frontend server
```
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
```
13.  copy the frontend code to html path
```
sudo cp -r * /var/www/html
```
14.  access the application with public ip or loadblancer url
15. sign up and login the appliaction


## Usage

- Run backend scripts as needed for database or S3 operations.
- Open HTML files in `Frontend/Frontend-code/` to view the web interface.
- Customize CSS files for styling changes.
- For S3 integration, review and configure the policy in `Frontend-S3/s3backendpolicys.txt`.

## Contributing

Feel free to fork the repository and submit pull requests for improvements or bug fixes.

