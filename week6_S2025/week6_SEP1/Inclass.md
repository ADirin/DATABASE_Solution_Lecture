# Lecture Exercise: Developing an Interactive Console-Based Java Application with CI/CD Pipeline  

## Objective  
Students will develop a simple interactive console-based Java application, apply unit testing and code coverage testing, integrate the project with GitHub, set up Jenkins for automated testing, perform remote testing using a `Jenkinsfile`, and finally, containerize the application using Docker.  

## Exercise Overview  

### 1. Develop an Interactive Console-Based Java Application  
- Create a Java application that prompts users to enter two numbers and performs basic arithmetic operations (addition, subtraction, multiplication, and division).  
- The application will continuously run until the user chooses to exit.  

### 2. Write Unit Tests and Coverage Tests  
- Use **JUnit 5** to create unit tests for key functionalities.  
- Apply **JaCoCo** (Java Code Coverage Tool) to measure test coverage.  

### 3. Set Up GitHub and Push the Code  
- Initialize a **Git** repository and push the project to **GitHub**.  
- Ensure a proper `.gitignore` file is set up.  

### 4. Implement Jenkins Freestyle Job for Automated Testing  
- Configure **Jenkins** to pull code from GitHub and run tests.  
- Set up a **Freestyle Job** to:  
  - Fetch the latest code.  
  - Run unit tests automatically.  
  - Publish test results and coverage reports.  

### 5. Implement Jenkins Pipeline with Jenkinsfile  
- Create a `Jenkinsfile` to define an automated build and test pipeline.  
- Push the `Jenkinsfile` to the **GitHub** repository.  
- Configure **Jenkins** to run tests using the `Jenkinsfile` from **SCM**.  

### 6. Containerize the Application with Docker  
- Write a `Dockerfile` to define the Java application environment.  
- Build and run the **Docker** image locally.  
