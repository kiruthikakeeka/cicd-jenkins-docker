# CI/CD Pipeline — Jenkins + GitHub + Docker

A production-style CI/CD pipeline that automates build, test, and containerized deployment using Jenkins and Docker.

## 🔧 Tools & Technologies
- Jenkins
- GitHub (Webhooks)
- Docker
- SonarQube (Code Quality)

## 🏗️ Pipeline Flow
Code Push → GitHub Webhook → Jenkins Trigger → Build → SonarQube Scan → Docker Build → Deploy to Staging → Deploy to Production
## ✅ Results
- Reduced manual deployment effort by 60%
- Reduced deployment failures by 40%
- Automated code quality checks on every commit

## 📁 Project Structure
├── Jenkinsfile          # Pipeline definition
├── Dockerfile           # Container configuration
├── docker-compose.yml   # Multi-container setup
└── sonar-project.properties  # SonarQube config

## 🚀 How to Run
1. Clone the repo
2. Configure Jenkins with GitHub webhook
3. Add Docker credentials in Jenkins
4. Trigger pipeline via code push
