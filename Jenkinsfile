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
        //docker.withRegistry("sarataha-docker-docker_jenkins_java_pipeline.bintray.io", "bintray") {
          //def app = docker.build("sarataha-docker-docker_jenkins_java_pipeline.bintray.io/demo/docker_jenkins_java_pipeline:${env.BUILD_NUMBER}")
          //def app = docker.build("docker_jenkins_pipeline:${env.BUILD_NUMBER}")
        //}
      docker.build("sarataha/docker_jenkins_java_pipeline:${env.BUILD_NUMBER}").push()
    }
  }
}
