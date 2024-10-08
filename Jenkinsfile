def COLOR_MAP = [
    'SUCCESS': 'good',
    'FAILURE': 'danger',
]

pipeline {
    agent any
    tools {
        maven "MAVEN3"
        jdk "OracleJDK17"
    }

    environment {
        SNAP_REPO = 'vprofile-snapshot'
        NEXUS_USER = 'admin'
        NEXUS_PASS = 'admin123'
        RELEASE_REPO = 'vprofile-release'
        CENTRAL_REPO = 'vpro-maven-central'
        NEXUS_IP = '172.31.16.20'
        NEXUS_PORT = '8081'
        NEXUS_GRP_REPO = 'vpro-maven-group'
        NEXUS_LOGIN = 'Nexuslogin'
        SONARSERVER = 'sonarserver'
        SONARSCANNER = 'sonarscanner'
    }

    stages {
        stage('Build'){
            steps {
                sh 'mvn -s settings.xml -DskipTests install'
            }
            post {
                success {
                    echo 'Archiving'
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
            
        }

        stage('Test') {
            steps {
                sh 'mvn -s settings.xml test'
            }
        }

        stage('Checkstyle Analysis') {
            steps {
                sh 'mvn -s settings.xml checkstyle:checkstyle'
            }
        }

        stage ('Sonar Analysis') {
            environment {
                scannerHome = tool "${SONARSCANNER}" 
            }
            steps {
                withSonarQubeEnv("${SONARSERVER}") {
                    sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=vprofile \
                    -Dsonar.projectName=vprofile \
                    -Dsonar.projectVersion=1.0 \
                    -Dsonar.sources=src/ \
                    -Dsonar.java.binaries=target/test-classes/com/visualpathit/account/controllerTest/ \
                    -Dsonar.junit.reportsPath=target/surefire-reports/ \
                    -Dsonar.jacoco.reportsPath=target/jacoco.exec \
                    -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml'''
                }
            }
        }

        stage ("Quality Gate") {
            steps {
                timeout(time:1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }

        stage ("Upload Artifact") {
            steps {
                nexusArtifactUploader(
                  nexusVersion: 'nexus3',
                  protocol: 'http',
                  nexusUrl: "${NEXUS_IP}:${NEXUS_PORT}",  
                  groupId: 'QA',
                  version: "${env.BUILD_ID}-${env.BUILD_TIMESTAMP}",
                  repository: "${RELEASE_REPO}",
                  credentialsId: "${NEXUS_LOGIN}", 
                  artifacts: [
                    [artifactId: 'vproapp',
                     classifier: '',
                     file: 'target/vprofile-v2.war',
                     type: 'war']
                  ]
                )
            }
        }
    }
    post {
        success{
            echo 'Slack Notifications'
            slackSend channel: '#dasmanth',
                color: COLOR_MAP[currentBuild.currentResult],
                message: "*${currentBuild.currentResult}:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} \n More info at: ${env.BUILD_URL}"
        }
    }
}























 pipeline {
    agentany {
    environment {

    }   
    parameters {

    } 
        tools {
            maven3 "mvn3"
            jdk11 "jdk11"
        }
    }
    stages {
        stage ('git checkout') {
            steps {
                sh "gitpull <gitrepourl>"
            }
        }
        stage ('code validate') {
            steps {
                sh "mvn validate"
            }
        }
    }
 }



 FROM nginx:latest
 COPY /etc/app 
 RUN apt get update
 RUN apt get install -y
 EXPOSE 80:80
 





 apiVersion: v1 
 kind: Deployment
 metadata:
     name: dev
     labels:
        dev: '01'
        company: talent
 spec:
     conta



 apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80














pipeline {
    agent any 
    tools {
        jdk "jdk11"
        maven "mvn3"
    }
    environment {
        SONARSERVER = 'admim'
        NEXUS_ID = 'admin'


    }
    parameters {

    }
    stages {
        stage ('code pull') {
            sh 'gitclone<githuburl>'
        }
        stage ('code validate') {
            sh 'mvn validate'
        }
        stage ('code compile') {
            sh 'mvn compile'
        }
        stage ('code test') {
            sh 'mvn test'
        }
        stage ('build') {
            sh 'mvn clean package'
        }
    }
}












FROM nginx:latest
LABEL dev:1
RUN yum update -y
RUN yum install nginx -y
EXPOSE 80
CMD ["nginx","-g", "daemon off:"]

FROM openjdk:8-jdk-alpine as builder
RUN mkdir -p /app/source
COPY . /app/source
WORKDIR /app/source
RUN ./mvnw clean package


FROM builder
COPY --from=builder /app/source/target/*.jar /app/app.jar
EXPOSE 8080
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom", "-jar", "/app/app.jar"]\




FROM ubuntu:latest
RUN apt-get update 
RUN apt-get install nginx:latest
COPY /usr/share/nginx
CMD ["nginx","-g","daemon off:"]





apiVersion: apps/v1
kind: Deployment
metadata: 
   name: nginx-deployment
   labels:
     app: nginx
spec:
  replicas: 5
  selector:
    matchLabels:
       app: nginx
  template:
    metadata:
       labels:
         app: nginx
    spec:
      containers:
      -  name: nginx
         image: nginx:latest
         ports:
         -  containerPort: 80













DevOps-Shack-Project --- k8s kubeadm join command



   join 172.31.40.50kubeadm:6443 --token 8jaarh.0vd93xk6bq5vxqec \
        --discovery-token-ca-cert-hash sha256:95bdae5d5fc65aedf6b6cd5b552aab0ea04b52cd8db7a4530eb9da665093182d


  sonarqube token (squ_aa4ba1a09a4036d33963a4276a2eaf7fedd7dd5e)   
  jenkins managed files --- (54ba0e0d-017f-4e1b-991b-76a5fcb88cd8)   

 pipeline {
    agent any
    tools {
        jdk 'jdk17'
        maven 'maven3'
    }
    environment {
        SCANNER_HOME= tool 'sonar-scanner'
    }

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Dasmanth/Boardgame.git'
            }
        }
        stage('Compile') {
            steps {
                sh "mvn compile"
                
            }
        }
        stage('Test') {
            steps {
                sh "mvn test"
                
            }
        }
        stage('File System Scan') {
            steps {
                sh "trivy fs --format table -o trivy-fs-report.html ."
                
            }
        }
        stage('SonarQube Analsyis') {
            steps {
                withSonarQubeEnv('sonar') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=BoardGame -Dsonar.projectKey=BoardGame \
                            -Dsonar.java.binaries=. '''
                }
            }
        }
        stage('Quality Gate') {
            steps {
                script {
                  waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token' 
                }
            }
        }
        stage ('Build') {
            steps {
            sh "mvn package"
           }
        }
        stage('Publish To Nexus') {
            steps {
               withMaven(globalMavenSettingsConfig: 'global-settings', jdk: 'jdk17', maven: 'maven3', mavenSettingsConfig: '', traceability: true) {
                    sh "mvn deploy"
                }
         
            }    
        }
        stage('Build & Tag Docker Image') {
            steps {
               script {
                   withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                            sh "docker build -t dasmanth/jenkins:latest ."
                    }
               }
            }
        }
        stage('Docker Image Scan') {
            steps {
                sh "trivy image --format table -o trivy-image-report.html dasmanth/jenkins:latest "
            }
        }
        stage('Push Docker Image') {
            steps {
               script {
                   withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                            sh "docker push dasmanth/jenkins:latest"
                    }
               }
            }
        }
    
        
    }
    
}










##Nginx docker file
FROM ubuntu:18.04
RUN apt get update
RUN apt get install nginx -y
COPY nginx.conf /etc/nginx
COPY server.conf /etc/nginx/conf.d
EXPOSE 80:80
CMD ["nginx","-g","daemon off;"]





##jenkins file


pipeline {
    agent any 
    tools {
        maven "maven3"
        jdk "jdk17"
    }
    environment {

    }
    stages {
        stage ('Git check out') {
            steps {
                sh git pull
            }
        }
    }
}


##k8s pod yaml file

apiVersion: v1                  apiVersion:
kind: Pod 
metadata:
    name:nginx
spec:
  containers:
  -  name: nginx
     image: nginx:latest
     ports:
     - containerPort: 80



     pipeline {
        agent any
        tools {
            jdk 'jdk11'
            maven 'maven3'
        }
        environment {
            SONAR_HOME= tool
        }
        stages {
            stage ('Git Checkout') {
                steps {
                    gitbranch: '<githubrepoURL>'
                }
            }
            stage ('Code compile') {
                steps {
                    sh "mvn compile"
                }
            }
            stage ('Code validate') {
                steps {
                    sh "mvn validate"
                }
            }
            stage ('Code test') {
                steps {
                    sh "mvn test"
                }
            }
            stage ('Sonar analysis') {
                steps {

                }
            }
            stage ('Quality gate') {
                steps {

                }
            }
            stage ('Build') {
                steps {
                    sh "mvn clean package"
                }
            }
            stage ('Pull artifact to nexus'){
                steps {
                    
                }
            }
            stage ('Docker image build & Tag') {
                steps {

                }
            }
        }
     }    




     FROM ubuntu:latest
     RUN apt get update -y 
     RUN apt get install nginx -y
     COPY nginx.conf /etc/nginx
     COPY server.conf /etc/nginx/nginx.conf 
     ADD 
     EXPOSE 80:80
     USER 
     CMD ["nginx","-g","daemon 0ff;"] 
                                                          

    apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
     apiVersion: apps/v1
     kind: Deployment 
     metadata: 
          name: nginx-deployment
          labels:
             app: nginx
     spec:
        replicas: 3
        selector:
           matchLabels:
              app: nginx 
        template:
           metadata:
              labels:
                 app: nginx
           spec:
              containers:
              -  name: nginx
                 image: nginx:latest
                 ports:
                 - containerPort: 80


apviVesrion: apps/v1
kind: Deployment
metadata:
    name: nginx
    labels:
       app: nginx
spec:
   replicas: 5
   selector:
     matchLabels:
        app: nginx 
    template:
       meatadata:
         labels:
           app: Nginx
       spec:
         containers:
         - name: nginx
           image: nginx:latest
           ports:
           - containerPort: 80


   FROM ubuntu:alpine
   RUN apt get update -y 
   RUN apt get install nginx -y 
   COPY nginx.conf /etc/         
   COPY server.cong /
   EXPOSE 80:80
   CMD ["nginx","-g","daemon off;"] 


   pipeline {
    aget any 
    tools {
        jdk "jdk11"
        maven "maven3"
    }
    environment {

    }
    stages {
        stage ('Gir Check out') {
            steps {
                
            }
        }
    }
   }      


---
- name: update web servers
  hosts: webservers
  remote_user: root 

  tasks:
  - name: ensure apache is at the latest version
    ansible.builtin.yum:
       name: httpd
       state: latest 

   - name: update database
     ansible.builtin.template:
        src: /srv/
        dest: /etc/ 



terraform {
    
}            