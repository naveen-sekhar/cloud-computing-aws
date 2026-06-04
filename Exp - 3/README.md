# Task 2: Add Users to Groups

You have recently hired user-1 into a role where they will provide support for Amazon S3. You will add them to the S3-Support group so that they inherit the necessary permissions via the attached AmazonS3ReadOnlyAccess policy.

> You can ignore any "not authorized" errors that appear during this task. They are caused by your lab account having limited permissions and will not impact your ability to complete the lab.

## Add user-1 to the S3-Support Group

1. In the left navigation pane, choose **User groups**.

2. Choose the **S3-Support** group link.

3. Choose the **Users** tab.

4. In the Users tab, choose **Add users**.

5. In the Add Users to S3-Support window, configure the following:

   - Select **user-1**

6. At the bottom of the screen, choose **Add users**.

7. In the Users tab you will see that user-1 has been added to the group.

---

## Add user-2 to the EC2-Support Group

You have hired user-2 into a role where they will provide support for Amazon EC2.

Using similar steps to the ones above, add **user-2** to the **EC2-Support** group.

user-2 should now be part of the EC2-Support group.

---

## Add user-3 to the EC2-Admin Group

You have hired user-3 as your Amazon EC2 administrator, who manage your EC2 instances.

Using similar steps to the ones above, add **user-3** to the **EC2-Admin** group.

user-3 should now be part of the EC2-Admin group.

1. In the navigation pane on the left, choose **User groups**.

Each Group should now have a **1** in the Users column, indicating the number of Users in each Group.

If you do not have a **1** beside each group, revisit the above instructions above to ensure that each user is assigned to a User group, as shown in the table in the Business Scenario section.

---

# Task 3: Sign-In and Test Users

In this task, you will test the permissions of each IAM User.

1. In the navigation pane on the left, choose **Dashboard**.

A **Sign-in URL for IAM users in this account** link is displayed on the right.

It will look similar to:

```text
https://123456789012.signin.aws.amazon.com/console
```

This link can be used to sign-in to the AWS Account you are currently using.

2. Copy the **Sign-in URL for IAM users in this account** to a text editor.

3. Open a private (Incognito) window.

### Mozilla Firefox

- Choose the menu bars at the top-right of the screen.
- Select **New private window**.

### Google Chrome

- Choose the ellipsis at the top-right of the screen.
- Select **New Incognito Window**.

### Microsoft Edge

- Choose the ellipsis at the top-right of the screen.
- Choose **New InPrivate window**.

### Microsoft Internet Explorer

- Choose the **Tools** menu option.
- Choose **InPrivate Browsing**.

4. Paste the IAM users sign-in link into the address bar of your private browser session and press Enter.

Next, you will sign-in as user-1, who has been hired as your Amazon S3 storage support staff.

---

## Sign-in as user-1

Sign-in with:

```text
IAM user name: user-1
Password: Lab-Password1
```

1. In the search box to the right of **Services**, search for and choose **S3** to open the S3 console.

2. Choose the name of the bucket that exists in the account and browse the contents.

Since your user is part of the S3-Support Group in IAM, they have permission to view a list of Amazon S3 buckets and the contents.

> Note: The bucket does not contain any objects.

Now, test whether they have access to Amazon EC2.

3. In the search box to the right of **Services**, search for and choose **EC2** to open the EC2 console.

4. In the left navigation pane, choose **Instances**.

You cannot see any instances. Instead, you see a message that states:

```text
You are not authorized to perform this operation.
```

This is because this user has not been granted any permissions to access Amazon EC2.

You will now sign-in as user-2, who has been hired as your Amazon EC2 support person.

---

## Sign Out user-1

1. At the top of the screen, choose **user-1**.

2. Choose **Sign Out**.

---

## Sign-in as user-2

1. Paste the IAM users sign-in link into your private browser tab's address bar and press Enter.

> Note: This link should be in your text editor.

Sign-in with:

```text
IAM user name: user-2
Password: Lab-Password2
```

2. In the search box to the right of **Services**, search for and choose **EC2** to open the EC2 console.

3. In the navigation pane on the left, choose **Instances**.

You are now able to see an Amazon EC2 instance because you have Read Only permissions. However, you will not be able to make any changes to Amazon EC2 resources.

> If you cannot see an Amazon EC2 instance, then your Region may be incorrect. In the top-right of the screen, pull-down the Region menu and select the region that you noted at the start of the lab (for example, N. Virginia).

4. Select the instance named **LabHost**.

5. In the **Instance state** menu above, select **Stop instance**.

6. In the **Stop Instance** window, select **Stop**.

You will receive an error stating:

```text
You are not authorized to perform this operation.
```

This demonstrates that the policy only allows you to view information, without making changes.

7. Choose the **X** to close the Failed to stop the instance message.

Next, check if user-2 can access Amazon S3.

8. In the search box to the right of **Services**, search for and choose **S3** to open the S3 console.

You will see the message:

```text
You don't have permissions to list buckets
```

because user-2 does not have permission to access Amazon S3.

You will now sign-in as user-3, who has been hired as your Amazon EC2 administrator.

---

## Sign Out user-2

1. At the top of the screen, choose **user-2**.

2. Choose **Sign Out**.

---

## Sign-in as user-3

1. Paste the IAM users sign-in link into your private window and press Enter.

2. Paste the sign-in link into the address bar of your private web browser tab again. If it is not in your clipboard, retrieve it from the text editor where you stored it earlier.

Sign-in with:

```text
IAM user name: user-3
Password: Lab-Password3
```

3. In the search box to the right of **Services**, search for and choose **EC2** to open the EC2 console.

4. In the navigation pane on the left, choose **Instances**.

As an EC2 Administrator, you should now have permissions to Stop the Amazon EC2 instance.

5. Select the instance named **LabHost**.

> If you cannot see an Amazon EC2 instance, then your Region may be incorrect. In the top-right of the screen, pull-down the Region menu and select the region that you noted at the start of the lab (for example, N. Virginia).

6. In the **Instance state** menu, choose **Stop instance**.

7. In the **Stop instance** window, choose **Stop**.

The instance will enter the stopping state and will shutdown.

8. Close your private browser window.
