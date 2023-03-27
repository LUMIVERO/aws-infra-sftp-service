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
* Create a user role - xcftp-access-role
* Create a user policy - xcftp-access-policy


Create an sftp user
---
* Create Create an sftp user within Secrets Manager service
* User record must be of format aws/transfer/s-62e9213fc1384fea9/xcftp where the the username will be xcftp. For example a new user record would be aws/transfer/s-62e9213fc1384fea9/xcftp2

Connecting to the sftp server
---
``` 
# use keys from onepass
sftp -i xcftp_user.pem xcftp@xcftp.lumivero.com 

# use password from onepass
sftp xcftp@xcftp.lumivero.com 
```

Confluence page
---
https://qsrinternational.atlassian.net/wiki/spaces/DEVOPS/pages/2601418790/SFTP+Service+Architecture+Diagram
