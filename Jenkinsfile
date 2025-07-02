node {

    stage('Git Pull') {
        git credentialsId: '68070b12-9864-43da-8415-35aa2e03dcc5', url: 'https://github.com/a-venkatesh-1998/maven-web-application.git'
    }

    stage('Prepare Maven') {
        def mavenHome = tool 'maven'
        env.M2_HOME = mavenHome
        env.PATH = "${mavenHome}/bin:${env.PATH}"
    }

    stage('Maven Build') {
        // Removed configFileProvider as per request
        sh "mvn clean package"
    }

    stage('SonarQube Report') {
        // Removed configFileProvider as per request
        sh "mvn sonar:sonar"
    }

    stage('Upload to Nexus') {
        // Keep configFileProvider here as per request
        configFileProvider([configFile(fileId: '6088a863-6ecc-4dc2-b790-d7b30fedfe4e', variable: 'MAVEN_SETTINGS')]) {
            sh "mvn deploy --settings $MAVEN_SETTINGS"
        }
    }
}
