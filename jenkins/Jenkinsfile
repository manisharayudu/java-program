pipeline { 

    agent { 

        docker { 

            image 'maven:3-alpine' 

            args '-v /root/.m2:/root/.m2' 

        } 

    } 

    stages { 

        stage('checkout') { 

            steps { 

                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'git', url: 'https://github.com/manisharayudu/java-program.git']]]) 

            } 

        } 

        stage('Build') { 

            steps { 

                sh 'mvn -B -DskipTests clean package' 

            } 

        } 

        stage('Test') { 

            steps { 

                sh 'mvn test' 

            } 

            post { 

                always { 

                    junit 'target/surefire-reports/*.xml' 

                } 

            } 

        } 

        stage('Deliver') { 

            steps { 

                sh './jenkins/scripts/deliver.sh' 

            } 

        } 

    } 

}
