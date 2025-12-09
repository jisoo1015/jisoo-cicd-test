pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // GitHub에서 코드 가져오기
                checkout scm
            }
        }

        stage('Build and Push to ECR') {
            steps {
                sh '''
                # 1. 변수 설정
                AWS_REGION=ap-northeast-2
                AWS_ACCOUNT_ID=723165663216
                ECR_REPO_NAME=jisoo01         
                ECR_URI=${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/${ECR_REPO_NAME}
                IMAGE_TAG=build-${BUILD_NUMBER}

                echo "ECR URI: $ECR_URI"
                echo "IMAGE TAG: $IMAGE_TAG"

                # 2. app 디렉토리로 이동해서 Docker 이미지 빌드
                cd app
                docker build -t $ECR_URI:$IMAGE_TAG .

                # 3. ECR 로그인
                aws ecr get-login-password --region $AWS_REGION \
                  | docker login --username AWS --password-stdin ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com

                # 4. ECR에 이미지 푸시
                docker push $ECR_URI:$IMAGE_TAG
                '''
            }
        }
    }
}

