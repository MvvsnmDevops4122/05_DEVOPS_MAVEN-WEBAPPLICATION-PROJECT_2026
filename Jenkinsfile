node {
    def mavenHome = tool name: 'mvn_3.9.15'

    stage('checkout') {
        git 'https://github.com/MvvsnmDevops4122/05_DEVOPS_MAVEN-WEBAPPLICATION-PROJECT_2026.git'
    }

    stage('Build') {
        sh "${mavenHome}/bin/mvn clean package"
    }

    stage('SonarQube Report') {
        sh "${mavenHome}/bin/mvn sonar:sonar"
    }

    stage('Upload to Nexus') {
        sh "${mavenHome}/bin/mvn deploy"
    }

    stage('Deploy to Tomcat') {
        sh '''
        curl -u satya:password \
        --upload-file target/maven-web-application.war \
        "http://54.91.76.99:8080/manager/text/deploy?path=/maven-web-application&update=true"
        '''
    }
}
