Hosting HTML websites on Amazon EC2 (Elastic Compute Cloud) involves setting up a web server on an EC2 instance and deploying your HTML files to that server. Here’s a comprehensive guide on how to do it, step by step.

### Step 1: Set Up an EC2 Instance

1. **Log into AWS Management Console** and navigate to the EC2 dashboard.
2. **Launch a new instance**:
   - Choose an Amazon Machine Image (AMI) suitable for web hosting, like Amazon Linux, Ubuntu, or any other Linux distribution that you're comfortable with.
   - Select an instance type (e.g., t2.micro for testing purposes under the free tier).
   - Configure instance details as needed (number of instances, network, subnet, IAM role, etc.).
   - Add storage if the default isn’t sufficient.
   - Configure a security group to allow HTTP (port 80) and SSH (port 22) access.
   - Review and launch the instance, selecting a key pair for SSH access. Make sure you have access to the key pair file (.pem).

### Step 2: Connect to Your Instance

- Use SSH to connect to your instance. On a Mac or Linux, open a terminal and use:
  ```bash
  ssh -i /path/to/your-key.pem ec2-user@<your-instance-public-dns>
  ```
- For Windows, you can use PuTTY or another SSH client, converting the `.pem` file to `.ppk` if necessary.

### Step 3: Install a Web Server

- **For Apache** (commonly used):
  ```bash
  sudo yum update -y   # For Amazon Linux
  sudo apt-get update  # For Ubuntu
  sudo yum install httpd -y   # For Amazon Linux
  sudo apt-get install apache2 -y  # For Ubuntu
  sudo systemctl start httpd     # For Amazon Linux
  sudo systemctl start apache2   # For Ubuntu
  sudo systemctl enable httpd    # To make Apache start on boot (Amazon Linux)
  sudo systemctl enable apache2  # To make Apache start on boot (Ubuntu)
  ```
- **For Nginx**:
  ```bash
  sudo yum install nginx -y    # For Amazon Linux
  sudo apt-get install nginx -y  # For Ubuntu
  sudo systemctl start nginx
  sudo systemctl enable nginx
  ```

### Step 4: Deploy Your HTML Files

- Move your HTML files to the web server directory:
  ```bash
  # For Apache on Amazon Linux
  sudo cp /path/to/your/files/* /var/www/html/
  
  # For Apache on Ubuntu
  sudo cp /path/to/your/files/* /var/www/html/

  # For Nginx (common directory on most Linux distributions)
  sudo cp /path/to/your/files/* /usr/share/nginx/html/
  ```
- Adjust file permissions and ownership as necessary:
  ```bash
  sudo chown -R apache:apache /var/www/html/  # For Apache on Amazon Linux
  sudo chown -R www-data:www-data /var/www/html/  # For Apache on Ubuntu
  sudo chown -R nginx:nginx /usr/share/nginx/html/  # For Nginx
  ```

### Step 5: Test Your Website

- Open a web browser and enter your EC2 instance’s public IP address or DNS name. You should see your HTML page(s) being served.

### Step 6: Manage DNS (Optional)

- If you have a domain name, you can point it to your EC2 instance’s IP address using your domain registrar’s management tools.

### Step 7: Monitor and Maintain

- Keep your system and software updated.
- Monitor your EC2 instance for performance and security.

This guide covers the basics of setting up an EC2 instance for hosting static HTML websites. For dynamic sites or applications, additional software and configurations (like databases and application servers) might be necessary.
