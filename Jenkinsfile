pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                echo 'This will be execute to test language parameter'
            }
        }
        stage('Python') {
            when { anyOf {
                environment name: 'LANGUAGE', value: 'Python'
                environment name: 'LANGUAGE', value: 'All'
            }
            }
            steps {
                print('write python code here')
            }
        }
        stage('C') {
            when { anyOf {
                environment name: 'LANGUAGE', value: 'C'
                environment name: 'LANGUAGE', value: 'All'
            }
            }
            steps {
                echo 'write C code here'
            }
        }
        stage('Bash') {
            when { anyOf {
                environment name: 'LANGUAGE', value: 'Bash'
                environment name: 'LANGUAGE', value: 'All'
            }
            }
            steps {
                echo 'Bash code here'
            }
        }
        stage('Java') {
            when { anyOf {
                environment name: 'LANGUAGE', value: 'Java'
                environment name: 'LANGUAGE', value: 'All'
            }
            }
            steps {
                echo 'Java code here'
            }
        }
    }
}


