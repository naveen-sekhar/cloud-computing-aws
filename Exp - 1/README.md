
# Task 1: Launch Your Amazon EC2 Instance

In this task, you will launch an Amazon EC2 instance with termination protection and stop protection. Termination protection prevents you from accidentally terminating the EC2 instance and stop protection prevents you from accidentally stopping the EC2 instance. You will also specify a User Data script when you launch the instance that will deploy a simple web server.

1. In the AWS Management Console choose **Services**, choose **Compute** and then choose **EC2**.

> Note: Verify that your EC2 console is currently managing resources in the N. Virginia (us-east-1) region. You can verify this by looking at the drop down menu at the top of the screen, to the left of your username. If it does not already indicate N. Virginia, choose the N. Virginia region from the region menu before proceeding to the next step.

2. Choose the **Launch instance** menu and select **Launch instance**.

---

## Step 1: Name and tags

Give the instance the name:

```text
Web Server
```

The Name you give this instance will be stored as a tag. Tags enable you to categorize your AWS resources in different ways, for example, by purpose, owner, or environment. This is useful when you have many resources of the same type — you can quickly identify a specific resource based on the tags you have assigned to it. Each tag consists of a Key and a Value, both of which you define. You can define multiple tags to associate with the instance if you want to.

In this case, the tag that will be created will consist of:

```text
Key: Name
Value: Web Server
```

---

## Step 2: Application and OS Images (Amazon Machine Image)

In the list of available Quick Start AMIs, keep the default **Amazon Linux AMI** selected.

Also keep the default **Amazon Linux 2023 AMI** selected.

An Amazon Machine Image (AMI) provides the information required to launch an instance, which is a virtual server in the cloud. An AMI includes:

- A template for the root volume for the instance (for example, an operating system or an application server with applications)
- Launch permissions that control which AWS accounts can use the AMI to launch instances
- A block device mapping that specifies the volumes to attach to the instance when it is launched

The Quick Start list contains the most commonly-used AMIs. You can also create your own AMI or select an AMI from the AWS Marketplace, an online store where you can sell or buy software that runs on AWS.

---

## Step 3: Instance type

In the Instance type panel, keep the default:

```text
t2.micro
```

selected.

Amazon EC2 provides a wide selection of instance types optimized to fit different use cases. Instance types comprise varying combinations of CPU, memory, storage, and networking capacity and give you the flexibility to choose the appropriate mix of resources for your applications. Each instance type includes one or more instance sizes, allowing you to scale your resources to the requirements of your target workload.

The t2.micro instance type has:

```text
1 virtual CPU
1 GiB memory
```

> Note: You may be restricted from using other instance types in this lab.

---

## Step 4: Key pair (login)

For **Key pair name - required**, choose:

```text
vockey
```

Amazon EC2 uses public–key cryptography to encrypt and decrypt login information. To ensure you will be able to log in to the guest OS of the instance you create, you identify an existing key pair or create a new key pair when launching the instance. Amazon EC2 then installs the key on the guest OS when the instance is launched. That way, when you attempt to login to the instance and you provide the private key, you will be authorized to connect to the instance.

> Note: In this lab you will not actually use the key pair you have specified to log into your instance.

---

## Step 5: Network settings

1. Next to **Network settings**, choose **Edit**.

2. For **VPC**, select:

```text
Lab VPC
```

The Lab VPC was created using an AWS CloudFormation template during the setup process of your lab. This VPC includes two public subnets in two different Availability Zones.

> Note: Keep the default subnet **PublicSubnet1**. This is the subnet in which the instance will run. Notice also that by default, the instance will be assigned a public IP address.

3. Under **Firewall (security groups)**, choose **Create security group** and configure:

```text
Security group name: Web Server security group
Description: Security group for my web server
```

A security group acts as a virtual firewall that controls the traffic for one or more instances. When you launch an instance, you associate one or more security groups with the instance. You add rules to each security group that allow traffic to or from its associated instances. You can modify the rules for a security group at any time; the new rules are automatically applied to all instances that are associated with the security group.

4. Under **Inbound security group rules**, notice that one rule exists.

Remove this rule.

---

## Step 6: Configure storage

In the Configure storage section, keep the default settings.

Amazon EC2 stores data on a network-attached virtual disk called Elastic Block Store.

You will launch the Amazon EC2 instance using a default:

```text
8 GiB
```

disk volume.

This will be your root volume (also known as a "boot" volume).

---

## Step 7: Advanced details

1. Expand **Advanced details**.

2. For **Termination protection**, select:

```text
Enable
```

When an Amazon EC2 instance is no longer required, it can be terminated, which means that the instance is deleted and its resources are released. A terminated instance cannot be accessed again and the data that was on it cannot be recovered. If you want to prevent the instance from being accidentally terminated, you can enable termination protection for the instance, which prevents it from being terminated as long as this setting remains enabled.

3. Scroll to the bottom of the page and then copy and paste the code shown below into the **User data** box:

```bash
#!/bin/bash
dnf install -y httpd
systemctl enable httpd
systemctl start httpd
echo '<html><h1>Hello From Your Web Server!</h1></html>' > /var/www/html/index.html
```

When you launch an instance, you can pass user data to the instance that can be used to perform automated installation and configuration tasks after the instance starts.

Your instance is running Amazon Linux 2023. The shell script you have specified will run as the root guest OS user when the instance starts.

The script will:

- Install an Apache web server (httpd)
- Configure the web server to automatically start on boot
- Run the Web server once it has finished installing
- Create a simple web page

---

## Step 8: Launch the instance

1. At the bottom of the Summary panel choose **Launch instance**.

You will see a Success message.

2. Choose **View all instances**.

3. In the Instances list, select **Web Server**.

Review the information displayed in the Details tab. It includes information about the instance type, security settings and network settings.

The instance is assigned a Public IPv4 DNS that you can use to contact the instance from the Internet.

To view more information, drag the window divider upwards.

At first, the instance will appear in a Pending state, which means it is being launched. It will then change to Initializing, and finally to Running.

4. Wait for your instance to display the following:

```text
Instance State: Running
Status Checks: 2/2 checks passed
```

Congratulations! You have successfully launched your first Amazon EC2 instance.

# Task 2: Monitor Your Instance

Monitoring is an important part of maintaining the reliability, availability, and performance of your Amazon Elastic Compute Cloud (Amazon EC2) instances and your AWS solutions.

1. Choose the **Status checks** tab.

With instance status monitoring, you can quickly determine whether Amazon EC2 has detected any problems that might prevent your instances from running applications. Amazon EC2 performs automated checks on every running EC2 instance to identify hardware and software issues.

Notice that both the **System reachability** and **Instance reachability** checks have passed.

2. Choose the **Monitoring** tab.

This tab displays Amazon CloudWatch metrics for your instance. Currently, there are not many metrics to display because the instance was recently launched.

You can choose the three dots icon in any graph and select **Enlarge** to see an expanded view of the chosen metric.

Amazon EC2 sends metrics to Amazon CloudWatch for your EC2 instances. Basic (five-minute) monitoring is enabled by default. You can also enable detailed (one-minute) monitoring.

3. In the **Actions** menu towards the top of the console, select:

```text
Monitor and troubleshoot > Get system log
```

The System Log displays the console output of the instance, which is a valuable tool for problem diagnosis. It is especially useful for troubleshooting kernel problems and service configuration issues that could cause an instance to terminate or become unreachable before its SSH daemon can be started.

If you do not see a system log, wait a few minutes and then try again.

4. Scroll through the output and note that the HTTP package was installed from the user data that you added when you created the instance.

```text
Console-Output
```

5. Choose **Cancel**.

6. Ensure **Web Server** is still selected.

Then, in the **Actions** menu, select:

```text
Monitor and troubleshoot > Get instance screenshot
```

This shows you what your Amazon EC2 instance console would look like if a screen were attached to it.

```text
Screen-shot
```

If you are unable to reach your instance via SSH or RDP, you can capture a screenshot of your instance and view it as an image. This provides visibility as to the status of the instance, and allows for quicker troubleshooting.

7. Choose **Cancel**.

Congratulations! You have explored several ways to monitor your instance.

---

# Task 3: Update Your Security Group and Access the Web Server

When you launched the EC2 instance, you provided a script that installed a web server and created a simple web page. In this task, you will access content from the web server.

1. Ensure **Web Server** is still selected.

Choose the **Details** tab.

2. Copy the **Public IPv4 address** of your instance to your clipboard.

3. Open a new tab in your web browser, paste the IP address you just copied, then press **Enter**.

### Question

Are you able to access your web server? Why not?

You are not currently able to access your web server because the security group is not permitting inbound traffic on port 80, which is used for HTTP web requests. This is a demonstration of using a security group as a firewall to restrict the network traffic that is allowed in and out of an instance.

To correct this, you will now update the security group to permit web traffic on port 80.

4. Keep the browser tab open, but return to the EC2 Console tab.

5. In the left navigation pane, choose **Security Groups**.

6. Select **Web Server security group**.

7. Choose the **Inbound rules** tab.

The security group currently has no inbound rules.

8. Choose **Edit inbound rules**, select **Add rule** and then configure:

```text
Type: HTTP
Source: Anywhere-IPv4
```

9. Choose **Save rules**.

10. Return to the web server tab that you previously opened and refresh the page.

You should see the message:

```text
Hello From Your Web Server!
```

Congratulations! You have successfully modified your security group to permit HTTP traffic into your Amazon EC2 Instance.

# Task 4: Resize Your Instance: Instance Type and EBS Volume

As your needs change, you might find that your instance is over-utilized (too small) or under-utilized (too large). If so, you can change the instance type. For example, if a t2.micro instance is too small for its workload, you can change it to an m5.medium instance. Similarly, you can change the size of a disk.

---

## Stop Your Instance

Before you can resize an instance, you must stop it.

When you stop an instance, it is shut down. There is no runtime charge for a stopped EC2 instance, but the storage charge for attached Amazon EBS volumes remains.

1. On the EC2 Management Console, in the left navigation pane, choose **Instances** and then select the **Web Server** instance.

2. In the **Instance state** menu, select **Stop instance**.

3. Choose **Stop**.

Your instance will perform a normal shutdown and then will stop running.

4. Wait for the Instance state to display:

```text
Stopped
```

---

## Change The Instance Type and Enable Stop Protection

1. Select the **Web Server** instance, then in the **Actions** menu, select:

```text
Instance settings > Change instance type
```

Configure:

```text
Instance Type: t2.small
```

2. Choose **Apply**.

When the instance is started again it will run as a t2.small, which has twice as much memory as a t2.micro instance.

> NOTE: You may be restricted from using other instance types in this lab.

3. Select the **Web Server** instance, then in the **Actions** menu, select:

```text
Instance settings > Change stop protection
```

4. Select **Enable** and then **Save** the change.

When you stop an instance, the instance shuts down. When you later start the instance, it is typically migrated to a new underlying host computer and assigned a new public IPv4 address. An instance retains its assigned private IPv4 address. When you stop an instance, it is not deleted. Any EBS volumes and the data on those volumes are retained.

---

## Resize the EBS Volume

1. With the **Web Server** instance still selected, choose the **Storage** tab.

2. Select the name of the **Volume ID**, then select the checkbox next to the volume that displays.

3. In the **Actions** menu, select **Modify volume**.

The disk volume currently has a size of **8 GiB**. You will now increase the size of this disk.

4. Change the size to:

```text
10
```

> NOTE: You may be restricted from creating Amazon EBS volumes larger than 10 GB in this lab.

5. Choose **Modify**.

6. Choose **Modify** again to confirm and increase the size of the volume.

---

## Start the Resized Instance

You will now start the instance again, which will now have more memory and more disk space.

1. In left navigation pane, choose **Instances**.

2. Select the **Web Server** instance.

3. In the **Instance state** menu, select **Start instance**.

Congratulations! You have successfully resized your Amazon EC2 Instance. In this task you changed your instance type from t2.micro to t2.small. You also modified your root disk volume from 8 GiB to 10 GiB.

---

# Task 5: Explore EC2 Limits

Amazon EC2 provides different resources that you can use. These resources include images, instances, volumes, and snapshots. When you create an AWS account, there are default limits on these resources on a per-region basis.

1. In the AWS Management Console, in the search box next to **Services**, search for and choose **Service Quotas**.

2. Choose **AWS services** from the navigation menu and then in the **AWS services Find services** search bar, search for:

```text
ec2
```

and choose:

```text
Amazon Elastic Compute Cloud (Amazon EC2)
```

3. In the **Find quotas** search bar, search for:

```text
running on-demand
```

but do not make a selection. Instead, observe the filtered list of service quotas that match the criteria.

Notice that there are limits on the number and types of instances that can run in a region. For example, there is a limit on the number of Running On-Demand Standard instances that you can launch in this region. When launching instances, the request must not cause your usage to exceed the instance limits currently defined in that region.

If you are the AWS account owner, you can request an increase for many of these limits.

---

# Task 6: Test Stop Protection

You can stop your instance when you do not need to access but you would still like to retain it. In this task, you will learn how to use stop protection.

1. In the AWS Management Console, in the search box next to **Services**, search for and choose **EC2** to return to the EC2 console.

2. In left navigation pane, choose **Instances**.

3. Select the **Web Server** instance and in the **Instance state** menu, select **Stop instance**.

4. Then choose **Stop**.

Note that there is a message that says:

```text
Failed to stop the instance i-1234567xxx.
The instance 'i-1234567xxx' may not be stopped.
Modify its 'disableApiStop' instance attribute and try again.
```

This shows that the stop protection that you enabled earlier in this lab is now providing a safeguard to prevent the accidental stopping of an instance. If you really want to stop the instance, you will need to disable the stop protection.

5. In the **Actions** menu, select:

```text
Instance settings > Change stop protection
```

6. Remove the check next to:

```text
Enable
```

7. Choose **Save**.

You can now stop the instance.

8. Select the **Web Server** instance again and in the **Instance state** menu, select **Stop instance**.

9. Choose **Stop**.

Congratulations! You have successfully tested stop protection and stopped your instance.
