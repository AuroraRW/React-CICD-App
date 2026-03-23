pipeline {
    agent any
    // environment{
    //     NETLIFY_SITE_ID = '68be4546-1f16-4c1d-a58e-18afc8935b82'
    //     NETLIFY_AUTH_TOKEN = credentials('tempToken')
    // }
    stages {
        // stage('Docker'){
        //     steps{
        //         sh 'docker build -t my-docker-image .'
        //     }
        // }

        // stage('Build') {
        //     agent {
        //         docker {
        //             image 'node:24.14.0-alpine'
        //             reuseNode true
        //         }
        //     }
        //     steps {
        //         sh '''
        //             # list all files
        //             ls -la
        //             node --version
        //             npm --version
        //             npm install
        //             # npm ci
        //             npm run build
        //             ls -la
        //         '''
        //     }
        // }

        // stage('Test') {
        //     agent {
        //         docker {
        //             image 'node:24.14.0-alpine'
        //             reuseNode true
        //         }
        //     }
        //     steps {
        //         sh '''
        //             test -f build/index.html
        //             npm test
        //         '''
        //     }
        // }

        // stage('Deploy') {
        //     agent {
        //         docker {
        //             // image 'node:24.14.0-alpine'
        //             image 'my-docker-image'
        //             reuseNode true
        //         }
        //     }
        //     steps {
        //         sh '''
        //             # npm install netlify-cli
        //             # node_modules/.bin/netlify --version
        //             # echo "Deploying to production. Site ID: $NETLIFY_SITE_ID"
        //             # node_modules/.bin/netlify status
        //             # # deploy to build folder
        //             # node_modules/.bin/netlify deploy --prod --dir=build

        //             ###### custom docker image
        //             netlify --version
        //             echo "Deploying to production. Site ID: $NETLIFY_SITE_ID"
        //             netlify status
        //             netlify deploy --prod --dir=build
        //         '''
        //     }
        // }
        stage('AWS'){
            agent {
                docker {
                    image 'amazon/aws-cli'
                    reuseNode true
                    args '--entrypoint=""'
                }
            }
            steps{
                withCredentials([usernamePassword(credentialsId: 'tempAWS', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')]) 
                {
                    // some block
                    sh '''
                        aws --version
                        aws s3 ls
                        echo "Hello S3!" > index.html
                        aws s3 cp index.html s3://temp2026-03-22/index.html
                    '''
                }
            }
        }
    }
}
