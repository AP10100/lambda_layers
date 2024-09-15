pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'ap-south-1' 
        LAMBDA_LAYER_NAME = 'testing_lambda_layer' 
        BUILD_DIRECTORY_PATH = "${WORKSPACE}/lambda-layer"
    }

    stages {
        stage('Build Layer') {
            steps {
                script {
                    // Create Lambda layer zip file
                    sh "mkdir -p ${BUILD_DIRECTORY_PATH}"
                    sh "zip -r ${BUILD_DIRECTORY_PATH}/${LAMBDA_LAYER_NAME}.zip ${WORKSPACE}/lambda-layer/*"
                }
            }
        }
        stage('Deploy Layer') {
            steps {
                script {
                    // Publish Lambda layer using AWS CLI
                    sh "aws lambda publish-layer-version --layer-name ${LAMBDA_LAYER_NAME} --zip-file fileb://${BUILD_DIRECTORY_PATH}/${LAMBDA_LAYER_NAME}.zip --compatible-runtimes nodejs16.x"
                }
            }
        }
    }
}
