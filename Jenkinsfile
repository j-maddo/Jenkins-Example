pipeline {
    // agent {
    //     docker {
    //         // Feel free to change the image for your project. Image taken from: https://github.com/cypress-io/cypress-docker-images/tree/master/browsers/node18.6.0-chrome105-ff104
    //         image 'cypress/base:18.6.0'
    //     }
    // }
    agent any

    tools {nodejs "19.5.0"}

    stages {
        // cleanup from folder on system remains from previous build like a cy beforeEach() to guarantee clean start
        stage('cleanup') {
            steps {
                // Jenkins function, https://www.jenkins.io/doc/pipeline/steps/workflow-basic-steps/#deletedir-recursively-delete-the-current-directory-from-the-workspace
                deleteDir()
            }
        }
        // first stage installs node dependencies and Cypress binary
        stage('build') {
            steps {
                // there a few default environment variables on Jenkins
                // on local Jenkins machine (assuming port 8080) see
                // http://localhost:8080/pipeline-syntax/globals#env
                echo "Running build ${env.BUILD_ID} on ${env.JENKINS_URL}"
                sh 'npm config ls'
            }
        }
        stage('test') {
            steps {
                // download NodeJS plugin for Jenkins to use the below steps
                // https://medium.com/appgambit/ci-cd-pipeline-for-a-nodejs-application-with-jenkins-fa3cc7fad13a
                sh 'npm i yarn'
                sh 'yarn'
                sh 'yarn run cypress:run'
            }
        }
        stage('deploy') {
            steps {
                echo 'Deploying'
            }
        }
    }
}