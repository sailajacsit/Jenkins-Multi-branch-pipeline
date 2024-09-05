Multi-Branch Jenkins Pipeline
This repository demonstrates a basic multi-branch Jenkins pipeline setup for building, testing, and deploying an application using parallel stages.

Jenkins Pipeline Overview
The pipeline contains three main stages:

Build: The project is built and the system details (hostname, working directory) are printed.
Test: Basic tests and delays are performed.
Deploy: Deployment steps, like printing a message, are carried out.
Pipeline Structure
groovy
Copy code
pipeline {
  agent any
  stages {
    stage('Build') {
      parallel {
        stage('Build') {
          steps {
            echo 'Building..'
            sh 'hostname'
            sh 'pwd'
            sh 'ls -al && hostname && pwd && cat /etc/passwd'
          }
        }

        stage('error') {
          steps {
            sh 'ls -al'
          }
        }

        stage('teststage') {
          steps {
            sh 'ls -al'
          }
        }
      }
    }

    stage('Test') {
      parallel {
        stage('Test') {
          steps {
            echo 'Testing..'
          }
        }

        stage('error') {
          steps {
            sleep 10
          }
        }
      }
    }

    stage('Deploy') {
      steps {
        echo 'Deploying....'
      }
    }
  }
}
Stages Explanation
Build Stage:

The Build stage runs parallel tasks to display system information (e.g., hostname, pwd, and system files).
The error and teststage steps simply list directory contents with ls -al.
Test Stage:

The Test step outputs a "Testing.." message.
The error step simulates a delay with sleep 10.
Deploy Stage:

Prints "Deploying...." as a placeholder for actual deployment logic.
How to Use
Jenkins Setup:

Ensure Jenkins is set up and configured to use a multi-branch pipeline.
Configure the repository URL in Jenkins under your pipeline job settings.
Run the Pipeline:

Once the job is triggered, Jenkins will execute the above stages, with parallel processing in the Build and Test stages.
Additional Notes
The pipeline can be customized further to include actual build, test, and deployment scripts.
The repository uses a multi-branch pipeline model, meaning Jenkins can track and execute this pipeline for different branches.
