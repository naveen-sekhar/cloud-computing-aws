
## Step 1: Open Lambda

In AWS search bar:

- Type: `Lambda`
- Click **Lambda** service.

---

## Step 2: Create Lambda Function

Click:

- **Create function**

Select:

- **Author from scratch**

Fill:

- **Function name:** `simple-demo`
- **Runtime:** Python 3.x
- **Permissions:** Choose **Use existing role**
- Select lab role (**LabRole/voclabs**)

Click:

- **Create function**

---

## Step 3: Add Simple Code

Delete existing code and paste:

```python
def lambda_handler(event, context):
    print("Hello Students - Lambda Working")
    return "Success"
```

Click:

- **Deploy**

Explain:

- This code is now stored in cloud.

---

## Step 4: Test Lambda

Click:

- **Test**

Create test event → keep default → **Test**

Output will show:

```text
Execution successful
```

---

## Step 5: Show Logs

Click:

- **Monitor → View CloudWatch logs**
- Open latest log stream.

Check for:

```text
Hello Students - Lambda Working
```
