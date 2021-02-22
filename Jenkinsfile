pipeline {
  environment {
    IMAGE_TAG = "us.gcr.io/${PROJECT}/${APP_NAME}:latest"
    JENKINS_CRED = "${PROJECT}"
  }
  agent {
    kubernetes {
      defaultContainer 'jnlp'
      yaml """
apiVersion: v1
kind: Pod
metadata:
labels:
  component: ci
spec:
  # Use service account that can deploy to all namespaces
  containers:
  - name: katalon
    image: katalonstudio/katalon
    imagePullPolicy: Always
    command:
    - cat
    tty: true
"""
}
  }
  stages {
    stage('katalon test') {
      steps {
        container('katalon') {
          sh """
              pwd
              katalon-execute.sh -browserType="Chrome (headless)" -retry=0 -statusDelay=15 -testSuitePath="Test Suites/Testrail cases adira/S3569 Hipster-pos"
             
              """
        }
      }
    }
   }
 }
