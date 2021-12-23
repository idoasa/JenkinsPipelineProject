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
    }
    post {
            always {
                echo 'Saving Results process..'
                sh '''
                   report_file="${HOME}/Documents/Deployment/report"
                   mkdir -p ${HOME}/Documets/Deployment/
                   if [ -f "${report_file}" ]
                   then
                       echo "file ${report_file} exists"
                   else
                       touch ${report_file}
                   fi
                   date >> ${report_file}
                   echo "USER-${USER} JOB_NAME-${JOB_NAME}" >> ${report_file}
                   echo "BuildNumber ${BUILD_NUMBER}" >> ${report_file}
                   cat "${WORKSPACE}/scripts/results" >> ${report_file}
                   echo "##############################" >> ${report_file}
               '''
            }
        }
    }
}


