# Terraform-Jenkins
This repository helps to build infrastructure such as AWS using Terraform with Jenkins Pipeline.
### Jenkins and Terraform and AWS


![Screen Shot 2021-07-01 at 4 43 17 PM](https://user-images.githubusercontent.com/87664653/173849388-eeff12a6-806a-4a1e-8c40-a25af72267c8.png)

## Jenkins

### Install Terraform plugin

To Install Terraform plugin,
Go to Manage Jenkins > Manage Plugins >Available > search Terraform.\

### Add AWS Credentiols

To configure AWS credentials in Jenkins:

1. Install Pipeline: AWS Steps
 navigate to Manage Jenkins > Manage Plugins under the Available tab of the Jenkins dashboard. Choose to install the Pipeline: AWS Steps plugin without a restart.

2. Add Aws credentials:
  You can add credentials by navigating to Manage Jenkins > Manage Credentials > Jenkins (global) > Global Credentials > Add Credentials. Choose kind as AWS credentials and enter "terraform-credentials" as the ID. Enter the access key ID and access key secret, then select OK.
![1cred](https://user-images.githubusercontent.com/87664653/176715051-1f5689b8-54b6-41a5-bc20-5540d8023519.png)
Note!
if you can not see the AWS credentials after adding the plugin.
please go to Manage Jenkins >  Configure Credential Providers > change Providers to all available and change types to all availlable.
![2 credentioalproviders](https://user-images.githubusercontent.com/87664653/176715202-9e3c1f24-1fac-4d49-a836-3f2692822b08.png)

### Add Terraform Pipeline

To add Terraform Pipeline,
Go to new item > Enter an item name > choose Pipline > Click OK

To add Jenkinsfile > Go to Pipline > Select "Pipline script from SCM" > Insert

Repository URL (<https://github.com/Omidznlp/Terraform-Jenkins.git>)


In Section Branches to build, Insert (*/master) > In Script Path, Insert (Jenkinsfile) > Click Save.


## Jenkins Nodes Label

I used master node to build Terraform Pipile, In Jenkins file into repositoy you can find it.

```
    agent {
      node {
        label "master"
      } 
`    }
```

I gave my Jenkins server the label "master," and then I ran Terraform on it.
Go to Manage Jenkins > Click "Manage nodes and clouds" > Select setting (left side of the list of nodes) > Under the label section, add "master" > Save it.

Note! Simply, you can change the label on the jenkins file or choose your node from your node lists from which you want to execute terraform and add the "master" label to it.

### Run Jenkins Pipline

![jeankens-pipline](https://user-images.githubusercontent.com/87664653/174333990-f6b5789d-13cc-4d00-817e-75516f4f0018.png)