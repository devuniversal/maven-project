pipeline {

agent any
tools {
    maven 'Maven3.3.9'
    jdk 'java8'
}
stages {

stage ('Build') {

steps {
echo "Checkout from Git"
checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '23a36a21-43a5-41e1-9bcc-a48c356f0a6d', url: 'https://github.com/devuniversal/maven-project.git']]])
echo "This is build stage"
sh label: '', script: 'mvn clean package checkstyle:checkstyle'


}
post {
    success {
        echo "Archive Artifacts"
        archive '**/webapp/target/*.war'
        echo "Publish Junit Report"
        junit '**/target/surefire-reports/*.xml'
        echo "Publish checkstyle Analisys Report"
        checkstyle canComputeNew: false, defaultEncoding: '', healthy: '', pattern: '', unHealthy: ''
        echo "Archive Artifacts"
        archiveArtifacts '**/webapp/target/*.war'
    }
}

}



stage ('Deploy-Dev') {

steps {

echo "This is Development Deployment Stage"

}

}



stage ('Deploy-Prod') {

steps {

echo "This is Production Deployment Stage"
timeout(time: 30, unit: 'SECONDS') {
input 'Do you want to Continue?'
}
build 'Deploy_War'
}

}

}

}
