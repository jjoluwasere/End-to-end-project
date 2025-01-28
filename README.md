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

2. Add the following to a **Dockerfile**:

![image](https://github.com/user-attachments/assets/f39789b2-7b67-46bb-ade5-b8141ae529e5)



3. Build the Docker image:

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

2. **Make the terraform files required for the deployment, in this i used 'main.tf, outputs.tf and variables.tf' as shown below:** <br><br>

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


## Step 5:  CI/CD Pipeline with GitHub Actions<br><br>

1. Set up GitHub Actions, create a **.github/workflows/ci-cd.yml** file: <br>

**Configuration for the build:**

![image](https://github.com/user-attachments/assets/5e8d9f50-525f-466e-a002-4ed23b14058e) <br>

**Configuration for the deploy:**

![image](https://github.com/user-attachments/assets/2769fe15-16a1-4123-81da-2d7457f780b5) <br><br>

Run **aws configure** then:
Make sure i have and input the following: the **AWS Access Key ID** and **AWS Secret Access Key** the region is 
**us-east-1** and select **json** <br><br>


Added AWS and Docker credentials as secrets in the GitHub repository.
Storing secrets such as passwords, API keys, and credentials securely is essential for maintaining both the scalability and security of applications.<br>
Hardcoding secrets directly into configuration files poses a significant risk, as it can lead to unauthorized access if these files are exposed. By leveraging GitHub Secrets, sensitive information is stored in an encrypted format, ensuring it remains secure while enabling easy integration into workflows.

![image](https://github.com/user-attachments/assets/85cb5184-13e7-41de-a385-2a74ceeb2683) <br>

![image](https://github.com/user-attachments/assets/7ad6b91b-4b81-4758-8087-69a2e7e6e850) <br>

The secrets i added will be securely accessed in my .github/workflows/ci-cd.yml file using ${{ secrets.<SECRET_NAME> }}. <br><br>


## Step 5: Kubernetes Deployment

1. Creating Kubernetes Files:

   Created the k8s/ directory and added:<br>

**deployment.yaml:** <br>

![image](https://github.com/user-attachments/assets/4c98c2ea-731e-4522-84db-6f8ef0b5ada2) <br>

**service.yaml** <br>

![image](https://github.com/user-attachments/assets/a7ec4192-b45f-4193-b5ee-6cbd535307b3) <br><br>

2. Deploying to Kubernetes:
   - applied the configurations
     - **kubectl apply -f k8s/**

   - Verified the deployment:
     - **kubectl get pods**
     - **kubectl get deployments**
     - **kubectl get service**

Also used YAML Lint to make sure everything was correct. <br>

![image](https://github.com/user-attachments/assets/1b732c3f-27fd-491c-8c29-150fc1776ccd) <br><br>


## Step 6: Push the Workflow

Commit and push the .github/workflows/ci-cd.yml file:

- **git add .github/workflows/ci-cd.yml**
- **git commit -m "Add GitHub Actions CI/CD pipeline"**
- **git push origin main**

Github Actions works its magic:

![image](https://github.com/user-attachments/assets/53296471-9274-403e-b742-fc3fcd64bc34) 

### Docker Build Issues:

Initial build failed due to an incorrect file path. Fixed by ensuring correct file hierarchy and paths in the Dockerfile.

### AWS Permissions:

Then i had issues with AWS permissions
Faced insufficient permissions error when deploying to AWS. This issue arose because my IAM user did not have the necessary permissions to access and manage the required AWS resources. <br>

![image](https://github.com/user-attachments/assets/25ef05c1-7f0e-45e9-bc39-c670661cf255) <br>


After identifying the root cause, a custom policy was created and attached to the IAM user. This policy granted explicit permissions for EKS, EC2, S3, and STS actions, ensuring that the pipeline could execute deployment steps seamlessly. <br>

![image](https://github.com/user-attachments/assets/4600980d-3dff-46ee-b9f0-e981944f4b60) <br>

After all that, Build was good however i did not setup the deploy properly, i needed to make an EKS cluster as i did not have any listed.<br>

![image](https://github.com/user-attachments/assets/e238182a-201f-49b7-a580-77fc2695395d) <br>

The **aws eks list-clusters** command has been executed. The output of the command is a JSON object with an empty clusters array, indicating that there are no Amazon EKS (Elastic Kubernetes Service) clusters available in my  AWS region (us-east-1). <br><br>

![image](https://github.com/user-attachments/assets/c6eb94cc-9a90-4724-b5e6-733fac213816) <br><br>

This shows the **eksctl create cluster** command being executed to create an Amazon EKS cluster named _ClusterForProject_ in the us-east-1 region with 2 managed nodes. The process includes setting up subnets, enabling Kubernetes, and creating CloudFormation stacks for the cluster and node group. The stack deployment has started. <br><br>

![image](https://github.com/user-attachments/assets/fa0e546b-4a26-427f-816a-dddfd1d99ec7)

Successfully created the clusters 2 nodes! This can be seen live in AWS CloudFormation. <br><br>

![image](https://github.com/user-attachments/assets/60e1905d-d6cd-4fec-835e-a7ce091009a9) <br>

After i noticed an error while creating, i had to update the kubernetes version to 1.3.1 as i was using 1.3.0.

![image](https://github.com/user-attachments/assets/d7c09d31-8647-4fde-ac5e-05b4f98d540b) <br><br>



After several tries and countless times troubleshooting by checking the logs and making sure everything is installed, it is successfully deployed.

![image](https://github.com/user-attachments/assets/872f3c69-3264-4658-b988-c63d77459837) <br>

![image](https://github.com/user-attachments/assets/45a1b927-bf4e-47a8-8ada-9aa9a74b6c1b) <br><br>

1. **Infrastructure:** Contains .terraform files and provider configurations for Terraform.
2. **End-to-end-project:** Includes .git for version control and a GitHub Actions workflow (ci-cd.yml) for continuous integration and deployment.
3. **app:** Contains application code, including index.html.
4. **docker:** Includes a Dockerfile for containerizing the application.
5. **k8s:** Contains Kubernetes configuration files (deployment.yaml and service.yaml) for deploying and exposing the application.
6. **terraform:** Includes Terraform files such as main.tf, variables.tf, outputs.tf, and state files for infrastructure management.
7. **README.md:** Documentation for the project.

![image](https://github.com/user-attachments/assets/834f3ea2-865d-42cd-9d5c-cae47f925890) <br><br>


![image](https://github.com/user-attachments/assets/9f6824b8-4af5-4922-bd26-96031758891c) <br><br>

To get the link for the application via a ALB. <br><br>

![image](https://github.com/user-attachments/assets/a2ef5138-d941-48a0-914c-5d51e811751c) <<br><br>
Everything works! <br><br>

## Conclusion <br>

This project provided valuable experience in integrating Docker, Kubernetes, Terraform, and AWS EKS into a seamless DevOps pipeline. I learned the importance of proper IAM permissions, YAML validation, and the role of secure secret management in ensuring successful deployments. The hands-on troubleshooting helped deepen my understanding of cloud infrastructure and CI/CD workflows, resulting in a successfully deployed application.




































  
