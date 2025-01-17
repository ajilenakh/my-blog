---
title: Book Library CI/CD Automation
type: page
---

## Introduction

Off the rip, this project is just me trying to get my hands dirty with the DevOps world. It marks the beginning of actively learning DevOps. So, first of all, I created a layout for building a book library web application using Spring. The idea was for users to search books and read them from the database, and for admins to upload books. Afterward, I created a Git repository and established two branches: `master` (default for production) and `development` (for dev). Then, I hosted an instance of Jenkins on my local machine to automate the deployment process. Although deploying a Spring Boot web app is tedious, it was a great learning opportunity.

## Jenkins Setup

Setting up Jenkins wasn't that complicated. I recommend reading the [Jenkins documentation](https://www.jenkins.io/doc/), but I followed this [guide](https://www.atlantic.net/dedicated-server-hosting/how-to-install-jenkins-on-arch-linux/) to set it up on my Arch Linux system. After installing Jenkins, I did the following:

### Set Up Credentials in Jenkins

For secure management of sensitive information (like database passwords), Jenkins provides a **Credentials Management** feature. This allows us to store and use sensitive data without exposing them in plaintext within the pipeline scripts.

###### 1. **Go to Manage Jenkins**
- From the Jenkins Dashboard, click on **Manage Jenkins** → **Configure Credentials**.

###### 2. **Add Credentials**
- Click on **(global)** or select the appropriate domain (if you are using domains to organize credentials).
- Click **Add Credentials**.
  - **Kind**: Select **Username with password**.
  - **Username**: Enter the database username.
  - **Password**: Enter the database password.
  - **ID**: Give the credentials a unique ID that will be referenced in your Jenkins pipeline script.
- Click **OK** to save the credentials.

### Create a Jenkins Pipeline Job

Now that Jenkins is installed and credentials are securely stored, let’s create a **Pipeline Job** to automate the process of building and deploying your application.

###### 1. **Create a New Pipeline Job**
- Go to the Jenkins Dashboard and click on **New Item**.
- Choose **Pipeline** and give your job a name (e.g., `book-library-pipeline`).
- Click **OK** to create the job.

###### 2. **Configure the Pipeline Script**
- After creating the pipeline job, you’ll be directed to the job configuration page.
- In the **Pipeline** section, select **Pipeline script** as the definition type.
- In the **Script** field, you will write the pipeline script (see next section for the script).

### Write the Jenkins Pipeline Script

This is the heart of your automation. The pipeline will automate the following:
- Pulling the latest code from your repository (via Git).
- Building the project using Maven.
- Running the Spring Boot application.

Here’s a **Jenkinsfile** example to accomplish that:

```groovy
pipeline {
    agent any

    environment {
        // Define the database host, port, and other non-sensitive info
        LIBRARY_MYSQL_DB_HOST = 'jdbc:mariadb://localhost'
        LIBRARY_MYSQL_DB_PORT = '3306'
    }

    stages {
        stage('Checkout') {
            steps {
                // Clone the repository from the 'master' branch
                git url: 'https://github.com/ajilenakh/book-library.git', branch: 'master'
            }
        }

        stage('Build') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'MYSQL_DB_CREDENTIALS', 
                                                      usernameVariable: 'LIBRARY_MYSQL_DB_USERNAME', 
                                                      passwordVariable: 'LIBRARY_MYSQL_DB_PASSWORD')]) {
                        sh 'mvn clean install'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'MYSQL_DB_CREDENTIALS', 
                                                      usernameVariable: 'LIBRARY_MYSQL_DB_USERNAME', 
                                                      passwordVariable: 'LIBRARY_MYSQL_DB_PASSWORD')]) {
                        sh 'mvn spring-boot:run'
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
    }
}
```
## Step 5: Test the Pipeline

- Save the Pipeline: After writing the pipeline script, click `Save`.

- Trigger the Build: Go to the pipeline job and click `Build Now` to start the pipeline manually.

- Check the Console Output: Monitor the build process by checking the Console  Output. This will show logs of each stage and any errors encountered during the process.


### Conclusion

After all this, I realized that Jenkins is not actually designed for running or deploying Spring Boot applications directly. It's primarily intended for automating tasks like testing and building. I was about to implement a webhook for automatic deployment, but I ran into issues with port forwarding for my Jenkins instance. You can read more about this problem [here](https://community.jenkins.io/t/in-progress-infinite-loop-while-run-spring-boot/18289).

Additionally, I set up two different environments using `application.properties` in Spring Boot. You can learn more about configuring multiple property files in Spring Boot [here](https://codesarray.com/view/Multiple-application-properties-file-in-spring-boot). In the development pipeline script, I added the line `spring.profiles.active=dev` to specify the active profile for the development environment.

```grovvy
    sh "echo 'spring.profiles.active=dev' >> src/main/resources/application.properties"
```

For more details, check out our repository:  
[GitHub Repository](https://github.com/ajilenakh/book-library.git)