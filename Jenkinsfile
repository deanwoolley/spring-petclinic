#!/bin/env groovy

pipeline {
  agent none

  environment {
    IMAGE = "liatrio/petclinic-tomcat"
  }

  stages {
    stage('Build') {
      agent any
      steps {
        sh 'mvn clean install'
      }
    }
    stage('Package') {
      agent any
      steps {
        script {
          echo env.BRANCH_NAME
          echo env.IMAGE
        }
      }
    }
    stage('Deploy to Dev') {
      agent any
      steps {
        script {   
          sh "docker rm -f petclinic-tomcat-temp || true"
          sh "docker run -d -p 9966:8080 --name petclinic-tomcat-temp ${env.IMAGE}:1.0.0-SNAPSHOT"

        }   
      }        
    }
    stage('Smoke-Test Dev') {
      agent any
      steps {
        //sample dummy step
        sh 'sleep 4'
      }
    }
    stage('Deploy to Perf Env') {
      agent any
      steps {
        //sample dummy step
        sh 'sleep 4'
      }
    }
    stage('Performance Test') {
      agent any
      steps {
        //sample dummy step
        sh 'sleep 4'
      }
    }
    stage('Deploy to UAT'){
      agent any
      steps {
        sh 'pwd'
        sh 'ls'
      }
    }
    stage ('Deploy to Prod') {
      agent any
      when {
              branch 'master'
      }
      steps{
        input ('Proceed?')
      }
    }
    stage('Smoke-Test Prod') {
      agent any
      when {
                branch 'master'
      }
      steps {
        echo "Smoke Testing Production"
        sh 'sleep 2'
      }
    }
  }
}
