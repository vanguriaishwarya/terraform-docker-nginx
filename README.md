## 🧱 Infrastructure as Code (IaC) with Terraform

## 🎯 Objective
Provision a local **NGINX Docker container** using **Terraform** as part of my DevOps Internship at Elevates Lab.

---

## 🧰 Prerequisites Installed

Before starting, I installed:

- ✅ [Terraform](https://developer.hashicorp.com/terraform/downloads) using Chocolatey:
  ```bash
  choco install terraform
✅ Docker Desktop and made sure it's running

✅ Git Bash terminal (for running Terraform and Docker CLI)

## 📁 Project Setup
Created a new folder on my Desktop:
copy
mkdir ~/Desktop/terraform-docker
cd ~/Desktop/terraform-docker
## Created a Terraform configuration file named main.tf:
- copy
  nano main.tf
- Pasted the following code in main.tf:
- Copy
  terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "~> 3.0.2"
    }
  }
}

provider "docker" {}

resource "docker_image" "nginx" {
  name         = "nginx:latest"
  keep_locally = false
}

resource "docker_container" "nginx_container" {
  name  = "nginx_terraform"
  image = docker_image.nginx.name

  ports {
    internal = 80
    external = 8080
  }
}
## 🚀 Commands I Executed
- Initialize Terraform:
- Copy
terraform init
## Preview what Terraform will do:
- Copy
terraform plan
## Apply the configuration (when prompted, typed yes):
- Copy
terraform apply

## ✅ Output
- Terraform pulled the nginx:latest Docker image.

- Created a container named nginx_terraform.

- Exposed it on http://localhost:8080.

## 📸 When I opened the browser and visited http://localhost:8080, I saw the NGINX welcome page.

## 🧹 Cleanup
- To destroy the container and remove the image:
- Copy
terraform destroy

## 📌 Notes
- I faced an error with docker_image.nginx.latest and fixed it by using docker_image.nginx.name.

- Used Git Bash to avoid path issues on Windows.

- Learned how Terraform interacts with Docker as a provider.
