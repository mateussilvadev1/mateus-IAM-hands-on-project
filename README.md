# When we first create our AWS account, we end up with what we call root account.

Which this means is that this root account have full access to our AWS Account. All sort of permissions are enabled.

This is a very dangeours account to use on a daily basis.

# Identity and Access Management - IAM

IAM appears to solve this problem.

We can create users to our AWS account to control which permissions they will have (even you as the owner of the account) as well which actions they're be capable to do on a daily routine.

I will give you one example.

The Human Resources of a companie have permissions to act in situations that belongs to Human Resources as well developers have permissions to perform the developers job inside the bussiness enviroment. 

Which means that HR doesn't have permissions to access developers resources. This concept is applyed to all the departments.

# IAM users and IAM groups

You can think in IAM Groups as deppartments of your companie. IAM users as the employees that belong to each deppartment. 

# IAM Roles

We also have the IAM Roles. Which is for those partners who can work with us as a guest. So they can perform acts in our behalf, inside our company, but just for a specific period of time we allow them to do it. 


# The idea of this project

I will build and IAM architecture of a company to show the hands-on practice of these concepts.

We will see across the screenshots provided in this repository, how I build a user for every employee of the companie, and also how I added all these users into organized groups, applying the best IAM practices for let your AWS Infrastructure as security as possible. 

# Hands-on - Developers

In my IAM project, I created a group called "Developers".

Permissions allowed:
- AmazonEC2FullAccess
- AmazonS3ReadOnlyAccess

This group has permissions to:
- Access EC2
- Start and stop instances

But it does NOT have permissions to:
- Access billing
- Manage IAM users

Then, I created a user called "john-dev" and added him to the Developers group.

As a result:
- John can work with EC2 resources
- But he cannot access sensitive parts of the account

This follows the principle of least privilege (Don't give more permission than a user really needs).

# Finance
I've also created a group for Finance.

Permissions allowed:
- Billing  
- AWSBillingReadOnlyAccess

This group has permissions to:
- Access the Billing dashboard
- View cost and usage reports

But it does NOT have permissions to:
- Access EC2
- Access S3 resources
- Manage infrastructure

Then, I created a user called "carlos-finance" and added him to the Finance group.

As a result:
- Carlos can monitor company costs
- But he cannot interact with technical resources


# DevOps / Admins

I created a group called "DevOps".

Permissions allowed:
- AdministratorAccess

This group has permissions to:
- Access EC2, S3, and CloudWatch
- Manage infrastructure resources

But it does NOT have permissions to:
- Access billing (optional, depending on company policy)

Then, I created a user called "ana-devops" and added her to the DevOps group.

As a result:
- Ana can manage and monitor the infrastructure
- But sensitive areas can still be restricted if needed

This follows the principle of least privilege.

# Juniors users

I created a group called "Interns".

This group has permissions to:
- Read-only access to selected services

But it does NOT have permissions to:
- Create, modify, or delete resources
- Access billing
- Manage infrastructure

Then, I created a user called "lucas-intern" and added him to the Interns group.

As a result:
- Lucas can learn and explore the environment safely
- But he cannot cause any impact on the infrastructure

This follows the principle of least privilege.

# Other groups configuration  
Other groups were created following the same process:

- Finance → Access to Billing dashboard  
  Policy: AWSBillingReadOnlyAccess

- DevOps → Full access to infrastructure services  
  Policy: AdministratorAccess  
  *(or combination of AmazonEC2FullAccess, AmazonS3FullAccess, CloudWatchFullAccess)*

- Interns → Read-only access  
  Policy: ReadOnlyAccess

All groups follow the principle of least privilege. Which means that we don't give more permission to an user than what he really needs.