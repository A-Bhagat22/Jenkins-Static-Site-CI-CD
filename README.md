 🚀 CI/CD Pipeline using Jenkins to Deploy a Static Website on AWS EC2

This project demonstrates a full CI/CD pipeline using **Jenkins**, **GitHub**, and **Apache Web Server** on an **AWS EC2 instance** to deploy a static website.

---

## 📂 Project Structure
jenkins-static-site-deploy/
├── index.html
├── css/
├── images/
├── Jenkinsfile
├── screenshots/
│ ├── jenkins-job.png
│ ├── website-output.png
└── README.md


---

## 🛠️ Tools & Technologies

- AWS EC2
- Jenkins
- GitHub
- Apache HTTP Server
- Shell scripting
- Linux permissions & directory management

---

## 🧠 Project Overview

Whenever new code is pushed to the GitHub repository, Jenkins pulls the changes, clears the old content from `/var/www/html`, and deploys the updated website — automating the complete flow.

---

## 🔧 Setup Instructions

### 1. Launch an EC2 Instance
- Amazon Linux or Ubuntu
- Open ports: 80 (Apache), 8080 (Jenkins)
- Create & attach a keypair

### 2. Install Required Packages

```bash
# Apache
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd

# Jenkins
sudo yum install java-11-openjdk -y
wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
sudo yum install jenkins -y
sudo systemctl start jenkins
sudo systemctl enable jenkins

### 3. Configure Jenkins
Unlock Jenkins using password from /var/lib/jenkins/secrets/initialAdminPassword

Install suggested plugins

Install Git plugin and Pipeline plugin

###📜 Jenkinsfile

pipeline {
    agent any

    stages {
        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/your-username/your-static-site-repo.git'
            }
        }

        stage('Clean Directory') {
            steps {
                sh 'sudo rm -rf /var/www/html/*'
            }
        }

        stage('Prepare Directory') {
            steps {
                sh 'sudo mkdir -p /var/www/html'
                sh 'sudo chown -R jenkins:jenkins /var/www/html'
            }
        }

        stage('Deploy Website') {
            steps {
                sh 'sudo cp -r * /var/www/html/'
            }
        }
    }
}

🌐 Live Demo
Static Website: http://**.***.***.***/

Jenkins Dashboard: http://**.***.***.***:8080/

✅ Conclusion
This project proves full CI/CD capability using Jenkins to automate web deployment. Ideal for DevOps fresher/interview showcase.
