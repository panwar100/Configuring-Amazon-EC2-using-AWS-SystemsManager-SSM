### Configuring-Amazon-EC2-using-AWS-SystemsManager-SSM
Configuring an Amazon EC2 instance using AWS Systems Manager (SSM) involves several steps. This service allows you to manage your EC2 instances at scale without needing to connect to them directly. Below are the steps to configure an EC2 instance through AWS Systems Manager
![0](https://github.com/panwar100/Configuring-Amazon-EC2-using-AWS-SystemsManager-SSM/assets/134361823/3ae9c33c-0d83-4a01-8c1e-d0625012d47d)
### Prerequisites:
* You should have an AWS account.
* You should have one or more EC2 instances launched and running.(use vpc default and In firewall(security group)-allow ssh,http,https traffic from the internet) 
  ![1](https://github.com/panwar100/Configuring-Amazon-EC2-using-AWS-SystemsManager-SSM/assets/134361823/59dab369-75b4-46da-a938-b6e818d4e848)


### 1.Create an IAM Role for Systems Manager:
* Go to the AWS Management Console.
*	Navigate to the Identity and Access Management (IAM) dashboard.
*	Create a new IAM role and attach the "AmazonEC2RoleforSSM" policy to it. This policy grants necessary permissions to Systems Manager for EC2 instances.
![2](https://github.com/panwar100/Configuring-Amazon-EC2-using-AWS-SystemsManager-SSM/assets/134361823/f3b9d479-463e-4d91-871d-f018ff182b7f)
![2 1](https://github.com/panwar100/Configuring-Amazon-EC2-using-AWS-SystemsManager-SSM/assets/134361823/09fdb8dc-5b69-4cd6-9fb4-793fe4ea3800)
![3](https://github.com/panwar100/Configuring-Amazon-EC2-using-AWS-SystemsManager-SSM/assets/134361823/e6a70637-5ff5-4c84-8cd3-68a83856a4fc)
![4](https://github.com/panwar100/Configuring-Amazon-EC2-using-AWS-SystemsManager-SSM/assets/134361823/28371d40-86c7-4f33-a926-87aa6a4d44b8)
*	Attach this IAM role to your EC2 instance when launching or modify the instance's IAM role.
  ![5](https://github.com/panwar100/Configuring-Amazon-EC2-using-AWS-SystemsManager-SSM/assets/134361823/968a985f-d0cf-4543-b408-30a5bd58ebda)
 	![6](https://github.com/panwar100/Configuring-Amazon-EC2-using-AWS-SystemsManager-SSM/assets/134361823/088da2d9-e0cd-4eea-9d27-f988688cca74)

### 2.Install the SSM Agent on the EC2 Instance:
*	SSH into your EC2 instance.
*	Download and install the SSM Agent by following the instructions provided in the AWS Systems Manager documentation for your specific operating system. The agent enables communication between the EC2 instance and Systems Manager.
(https://docs.aws.amazon.com/systems-manager/latest/userguide/agent-install-al.html)
* sudo yum install -y https://s3.region.amazonaws.com/amazon-ssm-region/latest/linux_amd64/amazon-ssm-agent.rpm
![7](https://github.com/panwar100/Configuring-Amazon-EC2-using-AWS-SystemsManager-SSM/assets/134361823/267bea9c-c44b-416e-8368-b76b72c110f3)

### 3.Verify SSM Agent Status:
* After installation, ensure that the SSM Agent is running and configured correctly by running the following command on your EC2 instance:
* sudo systemctl status amazon-ssm-agent
![8](https://github.com/panwar100/Configuring-Amazon-EC2-using-AWS-SystemsManager-SSM/assets/134361823/0754d9f0-ea61-4025-adb0-c1fe3b54592a)
The status should indicate that it is active and running.
### 4.Create an SSM Run Command:
Now that your EC2 instances are configured with SSM, you can use Systems Manager to perform various tasks, such as running commands or automating tasks:
*	In the AWS Systems Manager console, go to "Run Command" and create a new command.
  ![9](https://github.com/panwar100/Configuring-Amazon-EC2-using-AWS-SystemsManager-SSM/assets/134361823/1875341a-92f9-409a-84ed-0498a81a6e2b)
*	Select the EC2 instances you want to target.
![10](https://github.com/panwar100/Configuring-Amazon-EC2-using-AWS-SystemsManager-SSM/assets/134361823/abdb5d73-d3dd-4ded-a5be-dff1326a6aaa)
![12](https://github.com/panwar100/Configuring-Amazon-EC2-using-AWS-SystemsManager-SSM/assets/134361823/1f31d272-2631-4373-bc6f-3403ec1103d5)
![13](https://github.com/panwar100/Configuring-Amazon-EC2-using-AWS-SystemsManager-SSM/assets/134361823/d8ab5279-6253-465a-a509-7d4870420727)
* Choose the SSM document created in the previous step.
*	Configure any parameters or inputs required by the document.
![11](https://github.com/panwar100/Configuring-Amazon-EC2-using-AWS-SystemsManager-SSM/assets/134361823/f06d867d-025f-43fe-999b-69c505baadfc)
*	Start the command execution.

### 5.Monitor and View Results:
* You can monitor the progress and view the results of the SSM Run Command execution in the AWS Systems Manager console. This allows you to ensure that the desired configuration or automation task was executed successfully.
![14](https://github.com/panwar100/Configuring-Amazon-EC2-using-AWS-SystemsManager-SSM/assets/134361823/b1e23d19-3f64-4556-9020-1505e7059661)
* If you want to make some changes to the code, click Copy to new.
![15](https://github.com/panwar100/Configuring-Amazon-EC2-using-AWS-SystemsManager-SSM/assets/134361823/b263f411-444a-4538-8f0e-f8d23127a39b)
* change the command.
* ![16](https://github.com/panwar100/Configuring-Amazon-EC2-using-AWS-SystemsManager-SSM/assets/134361823/b3320fa1-8f1c-4e6e-b543-f7a0a1aa7a10)
![17](https://github.com/panwar100/Configuring-Amazon-EC2-using-AWS-SystemsManager-SSM/assets/134361823/591a6a10-e5e0-42a3-8d1d-baa423a42b21)
![18](https://github.com/panwar100/Configuring-Amazon-EC2-using-AWS-SystemsManager-SSM/assets/134361823/cdda3b75-0231-4a42-9d84-9277674563c5)

# AWS Systems Manager also provides capabilities for patch management, inventory management, and more. Explore the documentation and features to make the most of SSM for managing your EC2 instances efficiently and securely.
* [NOTICE:]If you connect ec2 ssh you can see that ssm agent is open.
![19](https://github.com/panwar100/Configuring-Amazon-EC2-using-AWS-SystemsManager-SSM/assets/134361823/cdbcbdff-0eda-47c3-b765-3cf8f0def221)
![20](https://github.com/panwar100/Configuring-Amazon-EC2-using-AWS-SystemsManager-SSM/assets/134361823/d1e9b380-99c1-4317-9c24-75c6eb375d06)
