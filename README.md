In our infrastructure, the security team wants to know if any of the users access key  in the security team is greater three days. If any users access key is more than three days, the security team will like the following:
1. Immediately delete the Access and Secret Key of the user if if it is greater than three days
2. Alert the security team about the incident and the remediation(1 point above)

The chief security wants the process to be automated

# Solution
The devices we will be making use of in this project will be

1. IAM-(Group)
   - If you don't have a "developers group", do the following:
        - Type IAM in the console
        - Select "user group" located on the left side
        - Click "Create Group" on the top right
        - Under "User group name" enter "developers"
        - Attach "AWSHealthFullAccess"

2. IAM-(Users)
   - If you don't have any users with programatic access attached to the developers group, do the following:
        - Type IAM in the console
        - Select "Users" located on the left side
        - Select "add user" located on the top left
        - Under "User name" enter a username for example "ab"
        - Under AWS access type select "Programmatic access"
        - assign any permission to this users
        - Under "Add user to group" check "developers" (The group we created in #1)
        - keep select "Next" until until we create user.
           (Create at least 2 users for this project )

3. IAM(Role)
  - If you don't have any lambda roles created for your users, do the following:
     - Type IAM in the console
     - Select "Roles" located on the left side
      - Click on "create roles"
      - Attach the awslambdaexecute, amazons3fullaccess and amazonsnsfullaccess policy to a lambda role.
      - Enter a role name for example 'lambda_access'.


4. LAMBDA
      - Create a Lambda function
      - Enter a function name for example 'scan-acccess-key-expiration'
      - Under 'Runtime' select 'python 3.7'.
      - Under 'permissions' select 'use an existing role' select the lambda role we created in #3 called 'lambda_access'.


5. SNS    
  - If you do not have an SNS topic, do the following:
     - Under 'Type' select 'Standard'
     - Create a Topic Name for example:'iamaccess'
     - Click 'Create topic'
     - Create subscription. select the 'topic arn' you just created.
     - Under 'protocol' select 'Email-JSON'
     - Under 'Endpoint' select the email of the security team that will be receiving the alert

Next step will be to go to lambda and start to execute the code that has been provided in the accessalert.py!
