pipeline {
  agent any
  options {
    skipDefaultCheckout(false)
  }
  environment {
    IMAGE = "meteor/filling-backend"
    TARGET_DEV = "containers-dev"
    TARGET_TST = "containers-test"
    TARGET_VAL = "containers-val"
    TARGET_PRD = "containers-prod"
  }
  stages {
    stage("Dev") {
      when {
        anyOf {
          allOf {
            not { expression { env.TAG_UNIXTIME } }
          }
        }
      }
      steps {
        script {
          config = [
            target: TARGET_DEV,
            image: IMAGE,
            tag: BRANCH_NAME + "-" + BUILD_NUMBER,
            dockerfile: "Dockerfile",
            artifactType: 'docker',
            pushToArtifactory: true,
            skipCleanup: true
          ]
        }
        dockerBuild(config)
      }
    }
}
}
