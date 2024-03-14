pipline {
    agent any
    stages {
        stage ('깃 업데이트'){
            steps {
                git url : 'https://github.com/emoee/kakaodevpipline.git', branch: 'main'
            }
        }
        stage ('도커 이미지 빌드, 푸시') {
            steps {
                sh '''
                docker build -t minsunnn/kakaodev:yellow .
                docker push minsunnn/kakaodev:yellow
                '''
            }
        }
        stage ('쿠버네티스 디플로이 서비스'){
            steps {
                sh '''
                kubectl create deployment deploy-yellow --image=minsunnn/kakaodev:yellow
                kubectl expose deployment deploy-yellow --type=LoadBalancer --port=8004 --target-port=80 -name=deploy-yellow-lb
                
                '''
            }
        }
    }
}
