pipeline {
agent any

```
environment {
    AWS_REGION = 'ap-south-1'
    ECR_REPO = '958941188585.dkr.ecr.ap-south-1.amazonaws.com/saleor'
    IMAGE_TAG = "${BUILD_NUMBER}"
}

stages {

    stage('Build Docker Image') {
        steps {
            sh '''
            docker build -t flask-app:${BUILD_NUMBER} ./app
            '''
        }
    }

    stage('Tag Image') {
        steps {
            sh '''
            docker tag flask-app:${BUILD_NUMBER} ${ECR_REPO}:${BUILD_NUMBER}
            '''
        }
    }

    stage('Push To ECR') {
        steps {
            sh '''
            aws ecr get-login-password --region ${AWS_REGION} | \
            docker login --username AWS --password-stdin 958941188585.dkr.ecr.ap-south-1.amazonaws.com

            docker push ${ECR_REPO}:${BUILD_NUMBER}
            '''
        }
    }
}
```

}
