
# Terraform AWS EC2 Deployment with Flask App

This project uses Terraform to automatically provision an AWS EC2 instance inside a VPC, with networking, security groups, and a Flask app deployment using provisioners.

## 🚀 What It Does

- Creates a custom VPC with a public subnet
- Attaches an Internet Gateway and routing
- Creates a security group to allow HTTP and SSH access
- Generates or uses an existing key pair for EC2 SSH access
- Provisions a t2.micro EC2 instance (Free Tier eligible)
- Uploads a `Flask` Python app (`app.py`) to the EC2 instance
- Automatically installs Python packages and runs the app

## 🔧 Files and Structure

```
terraform-ec2-flask/
├── main.tf        # Terraform configuration file
├── app.py         # Your Python Flask application
├── README.md      # This file
```

## 📦 Requirements

- AWS CLI configured (`aws configure`)
- Terraform installed
- A public-private SSH key pair in `~/.ssh/id_rsa` and `id_rsa.pub`
- `app.py` file in your project directory

## 💡 Key Features

- `aws_key_pair`: Uploads your public key to AWS
- `aws_instance`: Launches EC2 and runs remote provisioning steps
- `provisioner "file"`: Uploads your Flask app
- `provisioner "remote-exec"`: Installs Python, Flask, and runs the app

## 🖥️ Example Provisioning Steps

- `sudo apt update -y`
- `sudo apt-get install -y python3-pip`
- `pip3 install flask`
- `python3 app.py &` (runs in background)

## 🔐 Security

- Opens only ports 22 (SSH) and 80 (HTTP)
- You can tighten this by limiting the CIDR blocks

## 🏁 Getting Started

1. Place your `app.py` in the same directory as `main.tf`
2. Run the following commands:

```bash
terraform init
terraform apply
```

3. After deployment, visit the EC2 instance's public IP in your browser.

## 📌 Note

Make sure your `app.py` Flask app listens on:

```python
app.run(host='0.0.0.0', port=80)
```

## 🧹 Teardown

To destroy everything:

```bash
terraform destroy
```

---

✅ A great beginner-friendly project to understand AWS + Terraform + Python provisioning!
