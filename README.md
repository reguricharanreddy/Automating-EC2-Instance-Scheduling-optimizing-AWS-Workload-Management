# Automating-EC2-Instance-Scheduling-optimizing-AWS-Workload-Management

# Scenario :
In some companies, there is no need to run their EC2 instances 24/7; they require instances to operate during specific time periods, such as company working hours, from 8:00 AM in the morning to 5:00 PM in the evening. To address this scenario, I will implement two Lambda functions responsible for starting and stopping instances. These Lambda functions will be triggered by two CloudWatch Events in the morning and evening. This solution is fully serverless.
**Architecture**
![image](https://github.com/user-attachments/assets/b83bf1f0-92ba-49b8-8e36-b34a9fee102f)

# Steps :
## Step 1 :

Creating the Instance :

1.	Navigate to the EC2 Console.
2.	Follow the Outlined steps below.
3.	![image](https://github.com/user-attachments/assets/e8f74af6-a2e0-4725-94fb-c13f39dcaa0d)
4.	![image](https://github.com/user-attachments/assets/e6e9885b-0e4e-42df-b3d6-9fe2377d0e9b)
5.	![image](https://github.com/user-attachments/assets/77c09f9e-d346-4c64-ab47-7cc2c3cf8399)
6.	Give the existing key pair or create a new key pair
7.	![image](https://github.com/user-attachments/assets/87f2b5a7-0103-42bd-ad99-149c475d4e6f)
8.	![image](https://github.com/user-attachments/assets/168d39ad-4147-4e8f-97a7-e334596cec08)
9.	Click on Launch Instance.
10.	![image](https://github.com/user-attachments/assets/3da62df9-fec9-4665-9350-00b452c62577)
11.	After Launching an Instance , Instance will successfully runs.

## Step 2 :

Creating the Policy :

1.	Navigate to the IAM Console.
2.	Click on "Policies" and then Click on "Create policy"
3.	![image](https://github.com/user-attachments/assets/d33ef625-4301-4779-9a79-44bf65f3be5c)
4.	Select EC2 & Select Start Instances.
5.	![image](https://github.com/user-attachments/assets/499fce22-1a29-478a-b6ee-c127d7feb54e)
6.	Now Select DescribeInstances.
7.	![image](https://github.com/user-attachments/assets/24e2c8a3-541f-458b-ad02-401048dee5b0)
8.	![image](https://github.com/user-attachments/assets/e68076ed-be40-4f6f-a730-d8ebbf97947a)
9.	![image](https://github.com/user-attachments/assets/d857eb66-051f-4993-a4a8-7df707a09b91)
10.	![image](https://github.com/user-attachments/assets/786c3131-0693-42ff-8f3e-f41abc550012)
11.	
12.	.  Now we have created a policy for starting instances. We also need to create a   policy for stopping the instances. This is because we are going to create two Lambda functions: one for starting and one for stopping the instances. Each function will have its own role, and we will attach these two policies to their respective roles.
13. Now we are going to repeat the same steps for Creating Stopping Policy also.
14. Everything is same , Except Actions because we are going to stop the instance.
15. The Actions are DescribeInstances , StopInstances .
16. Keep your Policy name as "stop-ec2-instance".

## Step 3 :
Creating the Lambda functions :
1.	Navigate to the lambda Console.
2.	Click on create Lambda Function.
3.	Follow the Outlined steps below.


![image](https://github.com/user-attachments/assets/12ce2828-d4e3-4519-b19c-8e1a5bd8235f)

![image](https://github.com/user-attachments/assets/ea3d2488-055b-4fe1-8504-d7f43cb82bbb)

4.Click on Create Function.

![image](https://github.com/user-attachments/assets/025f82fb-6b8e-4eb1-9484-0fdd6631bc9c)

![image](https://github.com/user-attachments/assets/7cb91724-9834-4730-b6d6-34651ce322c0)

5.After the above step,Click on Deploy & go to configuration.

![image](https://github.com/user-attachments/assets/82993068-39e6-43ed-b6d8-4611cb78913d)

![image](https://github.com/user-attachments/assets/7c0929ec-f17e-4c61-8da4-fe12c7b8889c)

![image](https://github.com/user-attachments/assets/ce41af9e-a4d2-4623-8a1c-4fa34a05e5b4)

![image](https://github.com/user-attachments/assets/ff093552-d736-4ca9-ae28-8757bb8ba926)

![image](https://github.com/user-attachments/assets/913fa2a9-eeb8-4a20-b14e-9e82e96d8ffd)

![image](https://github.com/user-attachments/assets/319099de-f601-4a61-987e-fe35c6f49368)

6.Goto Permissions->Click on Add Permissions->Attach policies.

![image](https://github.com/user-attachments/assets/8c02b2d9-19f7-4584-bfb3-4674d28cf5a4)

7.Select the policy which is created before.and Add Permissions.

![image](https://github.com/user-attachments/assets/297dbefe-1e6d-45be-854a-ebd5e2e1765b)

8.Next Goto-> code -> and Test the python code.

![image](https://github.com/user-attachments/assets/c4d85896-5669-4cf7-a3e2-b97b1e917b7c)

 
9.In the above step we can see the result that our instance is in running state.
10.Now we Created alambda function for Starting Instance.
11.We have to Reapeat the same steps again to Create a Lambda function for Stopping Instance , Keep your lambda function name as "Stop-EC2-demo".
12.The only changes we have to make are to replace the default code with the 'stop-ec2-instance.py' code and attach the policy we created for stopping instances to the role of this Lambda function.
 
 ![image](https://github.com/user-attachments/assets/16ecb520-9f5b-4473-82d7-fb0371615990)

13.As demonstrated above, when I test my Python code, it runs successfully and stops the instance.
14.Now, we are ready to proceed and create schedules for this functions.

## Step 5 :
Creating the Schedules Using Cloud Watch :
1.	Navigate to the Cloud Watch Console.
2.	Follow the Outlined Steps below
   ![image](https://github.com/user-attachments/assets/0e75d718-c46e-4ede-9272-fb8d38fcd325)
   ![image](https://github.com/user-attachments/assets/9e0668b7-03c1-473a-b4e6-76ba1f077354)
   ![image](https://github.com/user-attachments/assets/7c2d2427-b3bd-45fd-a5ab-01bdd7b4deea)
   ![image](https://github.com/user-attachments/assets/61267d8c-a753-4459-8e83-7ae7af239ca9)
3.Chose Time Zone Asia/Kolkatta.

   ![image](https://github.com/user-attachments/assets/bf532d57-56a3-42cb-b31a-4d2607383fc1)
   ![image](https://github.com/user-attachments/assets/1132ab43-413a-4c2f-a1a9-4614b640ad0a)
   ![image](https://github.com/user-attachments/assets/4d9e2d87-708a-4cb8-8c5f-6e1c1feb911c)
   ![image](https://github.com/user-attachments/assets/4f4b7bd2-af4c-4d1b-8b1e-f77d20429bf8)
   ![image](https://github.com/user-attachments/assets/ae0c4bd8-e33a-4331-9718-0028dda1f188)
   ![image](https://github.com/user-attachments/assets/36fdc229-69f9-40f8-8395-3461aa47e0cf)
   ![image](https://github.com/user-attachments/assets/14490ffb-9fd4-4aff-baa6-095820dc2379)
   
4.	We have now created a schedule for starting the instance every day at 8:00 AM.
5.	Next, we need to create a schedule for stopping instances.
6.	To create the schedule for stopping instances, follow the same steps as for starting instance scheduling with a few changes, Keep your rule name as "stop-ec2-rule".
7.	The changes include modifying the scheduled time and selecting the appropriate scheduling function.
8.	We need to change the schedule time to 17:00 because it will stop the Lambda function at 17:00 IST (5:00 PM).

   ![image](https://github.com/user-attachments/assets/de5508a0-7cc4-4a46-934e-4f061a79d91b)

9.	We have to Change the Function as Stop-EC2-demo.
    
   ![image](https://github.com/user-attachments/assets/7b2889a8-4876-4515-b569-033660b03838)

10.Now, we have successfully created two schedules: one to start the instance every day at 8:00 AM and the other to stop the instance every day at 5:00 PM.

   ![image](https://github.com/user-attachments/assets/274a4475-c7a2-4294-8d09-1e8196812d23)

   ![image](https://github.com/user-attachments/assets/077b8c12-7aee-404e-ac95-6e79ae45c3e6)
 
11.	 In the above outlet the time is 01:06 AM so,the instance is stopped running due to Scheduling and it again start running at 08:00AM.

By implementing this project we will manage the AWS Workload management and optimize the EC2 Instance.



# Project Running State view during office hours

## Sample video:

https://github.com/user-attachments/assets/6256f373-592b-4990-8e53-13269506ee94



   

   
















