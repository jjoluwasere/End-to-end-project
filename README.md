# End-to-end-CI/CD-project
This project focuses on creating an end-to-end deployment pipeline for a static web application using tools like Terraform, Docker, Kubernetes, and GitHub Actions. The goal is to deploy a small static or web application using AWS Free Tier resources to avoid or reduce charges.


# Prerequsites

## 1. Install Required Tools:
      
      AWS CLI
      
      Terraform
      
      Docker Desktop for Mac
      
      kubectl
      
      eksctl
---
**AWS Account:**
Sign up for AWS Free Tier.

Have to create access keys (AWS Access Key ID and Secret Access Key).<br><br> 

**GitHub Account:**
Create a new repository for this project.<br><br>

## Step 2: Create a Static Web Application

1. Set up the app/ directory which i done in my mac terminal.<br>

     - **mkdir** -p devops-project-1/app
     - **cd** devops-project-1/app <br><br>
     
 
Write a simple web app, this is a simple **index.html** app accessible over the web.<br>


<img width="406" alt="image" src="https://github.com/user-attachments/assets/e7034635-8ca5-4823-a689-7de886555936" /><br>


Test app locally by opening **index.html** in a browser.<br><br>


## Step 3: Dockerize the Application

1. Create a Dockerfile:

   In the docker/ folder:

   - **mkdir ../docker**
  
   - **cd ../docker**<br><br>

Add the following to a **Dockerfile**:

![image](https://github.com/user-attachments/assets/f39789b2-7b67-46bb-ade5-b8141ae529e5)



Build the Docker image:

- **docker build -t static-app**.<br><br>



Created dockerfile and index.html static web app ready for deployment, included contents in the dockerfile to pull from docker.<br>

Run the Docker container:<br><br>


![image](https://github.com/user-attachments/assets/289f703e-6c60-4487-a333-7d493c37020d)

Ran this command to connect my app to be able to access nginx in the web browser.<br>

Open the 'http://localhost:8080' in your browser to verify.

![image](https://github.com/user-attachments/assets/11bc1b53-1bc0-47ac-a5d2-c85f9cf643e9)
**Successful, Docker acc name: jstandard9<br><br>**

- **docker login**

- **docker tag static-app jstandard9/static-app**

- **docker push jstandard9/static-app**

**Push the image to Docker Hub:** <br><br>
![image](https://github.com/user-attachments/assets/9a52c6fa-bbae-4bd3-a9a5-0113225f0e29) <br><br>



## Step 4:  Infrastructure Provisioning with Terraform<br><br>

1. Set up the terraform/ directory:<br><br>
   - **mkdir ../terraform**
   - **cd ../terraform** <br><br>


**Make the terraform files required for the deployment, in this i used 'main.tf, outputs.tf and variables.tf' as shown below:** <br><br>

![image](https://github.com/user-attachments/assets/0e12cbc6-6477-4bf0-903f-dfb4a6e22ba9)

This is what it should look like in vscode once that is completed.<br><br>

**This is the main.tf file** <br>

![image](https://github.com/user-attachments/assets/51d53117-944c-4a15-96b8-ea68aa067f46) <br><br>

**This is the variables.tf file** <br>

![image](https://github.com/user-attachments/assets/dd64e409-8586-41cc-baf8-1aa803b2d1b1) <br><br>

**This is the outputs.tf file** <br>

![image](https://github.com/user-attachments/assets/1ca24b1f-5aea-4c10-bf2b-5d92a3a3a2ea) <br><br>

After this i deployed my infrastructure. <br>

- **terraform init**
- **terraform plan**
- **terraform apply**

![image](https://github.com/user-attachments/assets/f0b66407-f882-4920-8ffe-f5da9c36afc9) <br><br>


## Step 4:  CI/CD Pipeline with GitHub Actions<br><br>



































  
