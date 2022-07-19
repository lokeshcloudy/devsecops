pipeline {
  agent any

  stages {
      stage('Build Artifact') {
            steps {
              sh "mvn clean package -DskipTests=true"
              archive 'target/*.jar' //so that they can be downloaded later
            }
        }
    
      stage('unit Test') {
            steps {
              sh "mvn test"
            }
        }
    
     stage('unit Test') {
            steps {
              withDockerRegistery([CredentialsId: "docker-hub", url: "public.ecr.aws/s2q9u1k0/devsecops"]) {
                sh 'docker build -t  public.ecr.aws/s2q9u1k0/devsecops:app:latest'
                sh 'docker push public.ecr.aws/s2q9u1k0/devsecops:app:latest'
              }

            }
        }
      
    }
}
