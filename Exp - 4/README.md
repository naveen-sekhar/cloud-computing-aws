# Lambda + S3 Demo

- When a file is uploaded to S3:
  - Lambda prints file name automatically.

- No server. Fully serverless.

---

## Steps

### Create S3 Bucket

- Search → **S3**
- Click **Create bucket**

**Bucket name:**

```text
student-lambda-demo-123
```

*(unique)*

- Keep default settings.
- Click **Create**.

---

### Create Lambda Function

- Search → **Lambda**
- Click **Create function**

Select:

- **Author from scratch**

**Function name:**

```text
s3-simple-demo
```

**Runtime:**

```text
Python 3.x
```

**Permissions:**

- Choose → **Use existing role**
- Select → **LabRole / voclabs role**

Click:

- **Create**

---

### Add Simple Code

Delete existing code and paste:

```python
def lambda_handler(event, context):
    for record in event['Records']:
        bucket = record['s3']['bucket']['name']
        file_name = record['s3']['object']['key']
        print("File uploaded:", file_name)
        print("Bucket name:", bucket)
    return "Done"
```

Click:

- **Deploy**

---

### Add S3 Trigger

In Lambda page:

- Click **Add trigger**

Select:

- **S3**

Choose your bucket.

**Event type:**

```text
PUT (ObjectCreated)
```

Click:

- **Add**

---

### Test

- Go to S3 bucket.
- Upload any file (image / txt).

Now go:

- **Lambda → Monitor → View CloudWatch logs**
- Open latest log stream.

You will see:

```text
File uploaded: test.txt
Bucket name: student-lambda-demo-123
```
