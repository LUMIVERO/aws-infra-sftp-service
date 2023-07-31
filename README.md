Cloud formation stack name
---
xcftp-credentials


Automation Steps: 
---
* Use aws-transfer-custom-idp-secrets-manager-apig.template.yml cloud formation yaml to spin up/tear down all the resources for the sftp server
* Provisioned resources
    * API Gateway
    * AWS Transfer Family
    * Lambda Application
    * Secrets Manager
    * A bunch of roles, policies and cloudwatch resources

Manual steps
---
* Create an S3 bucket - xcftp.lumivero.com
* Create a user role
* Create a user policy
* Create an sftp user
    * Create Create an sftp user within Secrets Manager service
    * User record must be of format aws/transfer/s-62e9213fc1384fea9/xcftp where the the username will be xcftp

Existing users
---
* xcftp user
    * aws/transfer/s-62e9213fc1384fea9/xcftp
    * xcftp-access-role
    * xcftp-access-policy
* xcftp user-reader
    * aws/transfer/s-62e9213fc1384fea9/xcftp-reader
    * xcftp-access-role-read
    * xcftp-access-policy-read
* xcftp user-uploader (only allow uploads into the upload folder in the S3 bucket)
    * aws/transfer/s-62e9213fc1384fea9/xcftp-uploader
    * xcftp-access-role-upload
    * xcftp-access-policy-upload    

User setup
---
Each user created under aws/transfer/s-62e9213fc1384fea9/[username] must have the following secrets setup
    
    * Password
    * Role (e.g. xcftp-access-role-upload ARN)
    * HomeDirectory (/xcftp.lumivero.com/contents)
    * PublicKey (key generated for the user using ssh-keygen -t ed25519 -f xcftp-reader -C "username as comment". Store the public key here and private key in onepass)

Connecting to the sftp server
---
``` 
# use keys from onepass
sftp -i xcftp_reader.pem xcftp@xcftp.lumivero.com 

# use password from onepass
sftp xcftp-reader@xcftp.lumivero.com 
```

Confluence page
---
https://qsrinternational.atlassian.net/wiki/spaces/DEVOPS/pages/2601418790/SFTP+Service+Architecture+Diagram
