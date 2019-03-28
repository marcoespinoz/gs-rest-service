node {
   def mvnHome = tool 'M3'

   stage('Checkout Code') { 
      git 'https://github.com/marcoespinoz/gs-rest-service.git'
   }
   stage('JUnit Test') {
      if (isUnix()) {
         sh "cd complete/ && '${mvnHome}/bin/mvn' clean test"         
      }
   }
   stage('Deployment') {
      if (isUnix()) {
         
         sh "cd complete/ &&  '${mvnHome}/bin/mvn' clean install"
      }
   }
   stage('Build docker image') {
      if (isUnix()) {
         sh "cp Dockerfile /var/lib/jenkins/.m2/repository/org/springframework/gs-rest-service/0.1.0/"
         sh "docker build -t 519901771307.dkr.ecr.us-west-2.amazonaws.com/reto:'${VERSION}' /var/lib/jenkins/.m2/repository/org/springframework/gs-rest-service/0.1.0/"
         sh "docker push 519901771307.dkr.ecr.us-west-2.amazonaws.com/reto:'${VERSION}'"
      }
   }
}
 /*
   stage('Build docker image') {
      if (isUnix()) {
         // sh "eval $(aws ecr get-login --region us-west-2 | sed -e 's/-e none//g')"
         sh "cp Dockerfile /var/lib/jenkins/.m2/repository/com/example/java-maven-junit-helloworld/2.0-SNAPSHOT"
         sh "docker build -t 519901771307.dkr.ecr.us-west-2.amazonaws.com/reto:v2 /var/lib/jenkins/.m2/repository/com/example/java-maven-junit-helloworld/2.0-SNAPSHOT/"
         
      } 
   }
  */
