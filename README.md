# docker-jenkins-java-pipeline

== Manual Steps

. *Start database*: `docker run -d --name db -p 8091-8093:8091-8093 -p 11210:11210 sarataha/oreilly-couchbase:latest`
. *Run app*
.. Using Maven
... *Build app*: `mvn -f webapp/pom.xml clean package`
... *Run app*: `mvn -f webapp/pom.xml exec:java -DskipTests`
... *Run test*: `mvn -f webapp/pom.xml test`
.. Using Docker
... *Build app*: `docker-compose build app`
... *Run app*:
+
```
docker-compose run -e DB_URI=`docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' db` app
```
+
... *Run test*: `mvn test`

== Jenkins

=== Configure

. Download Jenkins, this was tested with 2.21[http://mirrors.jenkins-ci.org/war/2.21/jenkins.war].
. Start Jenkins: `JENKINS_HOME=~/.jenkins java -jar ~/Downloads/jenkins-2.21.war --httpPort=9090`
. Create First Admin User, `Save and Finish`.
. Install suggested plugins
. `Manage Jenkins`, `Global Tool Configuration`, configure Maven, use name `Maven3` (this name is used in `Jenkinsfile`)
. `Manage Jenkins`, `Manage Plugins`, `Available`, install `CloudBees Docker Pipeline` plugin, `Install without restart`, select `Restart Jenkins`

=== Create Project

. Create a new project of the type `Pipeline`
. Configure git repo
. `Build Now`