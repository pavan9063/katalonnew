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
              katalonc -noSplash -runMode=console -projectPath="/home/jenkins/agent/workspace/katalon-job/ui testing sample botique/ui testing sample botique.prj" -retry=0 -testSuitePath="Test Suites/sample-testsuite/sample-1-cmd-orange" -executionProfile="default" -browserType="Chrome (headless)" -apiKey="82bbb2f3-c47a-4e89-bd4c-74d36b2b1241"
             
              """
        }
      }
    }
   }
 }
