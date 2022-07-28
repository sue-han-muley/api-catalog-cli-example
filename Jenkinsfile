pipeline {
    agent any

    tools {nodejs "NodeJS"}

    environment {
        ANYPOINT_ORG_ID = '6235ea6d-eb48-4cf9-a8f0-5f77018fbda2'
        CATALOG_DESCRIPTOR = './descriptor.yaml' 
     }
     stages {
        // stage('Build') {
        //     steps {
        //         nodejs(nodeJSInstallationName: 'Node 18.x', configId: '<config-file-provider-id>') {
        //             sh 'npm config ls'
        //         }
        //     }
        // }

        stage('API Cataloging') {
            steps {
                sh 'npm install -g api-catalog-cli@latest'

                withCredentials([
                    usernamePassword(credentialsId: 'anypoint.credentials',
                    usernameVariable: 'ANYPOINT_USERNAME',
                    passwordVariable: 'ANYPOINT_PASSWORD')
                ]) {
                    sh 'api-catalog publish-asset -d $CATALOG_DESCRIPTOR --organization="$ANYPOINT_ORG_ID" --username="$ANYPOINT_USERNAME" --password="$ANYPOINT_PASSWORD"'
                }
            }
        }
    }
}