Here is a step-by-step guide to launch an Ubuntu EC2 instance in AWS:

### Step 1: Login to AWS Console

1. Open AWS Management Console.
2. Navigate to [Amazon EC2](https://console.aws.amazon.com/ec2/?utm_source=chatgpt.com).
3. Select the AWS Region where you want to create the instance.

### Step 2: Launch Instance

1. Click **Launch Instance**.
2. Enter a name, for example:

   ```
   Ubuntu-Server
   ```

### Step 3: Select AMI (Operating System)

Under **Application and OS Images (AMI)**:

* Choose **Ubuntu Server 24.04 LTS** or **Ubuntu Server 22.04 LTS**.

Use:

* Ubuntu Server 24.04 LTS
  or
* Ubuntu Server 22.04 LTS

### Step 4: Select Instance Type

For Free Tier:

* Choose **t2.micro** (older free tier)
* Or **t3.micro** (if available under your account benefits)

Use:

* t2.micro

### Step 5: Create Key Pair

1. Under **Key Pair**, click **Create new key pair**.
2. Name:

   ```
   MyKeyPair
   ```
3. Key Pair Type: RSA
4. Private Key Format:

   * `.pem` for Linux/macOS
   * `.ppk` for PuTTY on Windows
5. Download and save the key securely.

### Step 6: Configure Network Settings

Click **Edit** and configure:

#### Create Security Group

Allow:

| Type  | Protocol | Port |
| ----- | -------- | ---- |
| SSH   | TCP      | 22   |
| HTTP  | TCP      | 80   |
| HTTPS | TCP      | 443  |

For SSH:

* Source = **My IP** (recommended)

### Step 7: Configure Storage

Default:

* 8 GB GP3 storage

For practice:

* Keep default settings.

### Step 8: Launch

Review settings and click:

```
Launch Instance
```

Wait 1–2 minutes until the instance state becomes **Running**.

---

## Connect to Ubuntu Instance

### Get Public IP

EC2 Dashboard → Instances → Select instance → Copy **Public IPv4 Address**

### Windows PowerShell

Navigate to the folder containing your `.pem` file:

```powershell
ssh -i "MyKeyPair.pem" ubuntu@<PUBLIC-IP>
```

Example:

```powershell
ssh -i "MyKeyPair.pem" ubuntu@54.123.45.67
```

If you get a permission error on Windows:

```powershell
icacls MyKeyPair.pem /inheritance:r
icacls MyKeyPair.pem /grant:r "%USERNAME%:R"
```

---

## Verify Connection

After login:

```bash
whoami
hostname
lsb_release -a
```

Expected user:

```bash
ubuntu
```

---

## Update the Server

```bash
sudo apt update
sudo apt upgrade -y
```

Check version:

```bash
uname -a
```

Since you've been practicing Linux, AWS, SSH, and MySQL recently, a good next task after launching the instance is:

```bash
sudo apt install nginx -y
```

Then open:

```
http://<PUBLIC-IP>
```

You should see the Nginx welcome page, confirming your EC2 instance is accessible from the internet.
