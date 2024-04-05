```
pipeline {
    agent any

    environment {
        TOMCAT_HOST = 'your_tomcat_server_ip'
        TOMCAT_PORT = '8080' // Default Tomcat port
        TOMCAT_USERNAME = 'your_ssh_username'
        TOMCAT_PASSWORD = credentials('your_ssh_password_credentials_id')
        WAR_FILE = 'your_web_app.war'
        TOMCAT_WEBAPPS_DIR = '/path/to/tomcat/webapps' // Path to the webapps directory in Tomcat
    }

    stages {
        stage('Build') {
            steps {
                // You can add your build steps here (e.g., Maven, Gradle, etc.)
                // Example:
                // sh 'mvn clean package'
                // Make sure your WAR file is generated and stored in your workspace
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Copy the WAR file to the Tomcat server
                    sh "scp -o StrictHostKeyChecking=no -P ${TOMCAT_PORT} ${WAR_FILE} ${TOMCAT_USERNAME}@${TOMCAT_HOST}:${TOMCAT_WEBAPPS_DIR}"

                    // Restart Tomcat
                    sh "sshpass -p '${TOMCAT_PASSWORD}' ssh -o StrictHostKeyChecking=no -p ${TOMCAT_PORT} ${TOMCAT_USERNAME}@${TOMCAT_HOST} 'sudo systemctl restart tomcat'"
                }
            }
        }
    }
}

```
