node {
  checkout scm
  env.PATH = "${tool 'Maven3'}/bin:${env.PATH}"
  stage('Compile') {
    dir('webapp') {
      sh 'mvn clean package'
      junit '**/target/surefire-reports/*.xml'
    }
  }

  stage('Create Docker Image') {
    dir('webapp') {
      docker.build("sarataha/docker-jenkins-java-pipeline:${env.BUILD_NUMBER}").push()
    }
  }
}
