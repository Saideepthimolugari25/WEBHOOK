pipeline {
    agent any

    triggers {
        githubpush()
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                bat '''
                    echo WORKSPACE=%WORKSPACE%
                    cd src

                    echo Compiling Java project...
                    javac hello/Hello.java
                '''
            }
        }

        stage('Run') {
            steps {
                bat '''
                    cd src
                    echo Running app...

                    java -cp . hello.Hello
                '''
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'src/hello/*.class', fingerprint: true
            }
        }
    }
}
