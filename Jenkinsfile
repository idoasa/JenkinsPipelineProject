pipeline {
    agent {label 'slave01'}

    stages {
         stage('Build') {
            steps {
                echo "Build process.."
                sh '''
                    cd ${WORKSPACE}/scripts/
                    chmod 755 *
                    date > results
                  '''
            }
        }
        stage('Python') {
            when { anyOf {
                environment name: 'LANGUAGE', value: 'Python'
                environment name: 'LANGUAGE', value: 'All'
            }
          }
            steps {
                sh '''
                    cd ${WORKSPACE}/scripts/
                    ./pythonscript.py >> results
                  '''
            }
        }
        stage('C') {
            when { anyOf {
                environment name: 'LANGUAGE', value: 'C'
                environment name: 'LANGUAGE', value: 'All'
            }
          }
            steps {
                sh '''
                    cd ${WORKSPACE}/scripts/
                    gcc -o Cscript Cscript.c
                    ./Cscript >> results
                  '''
            }
        }
        stage('Bash') {
            when { anyOf {
                environment name: 'LANGUAGE', value: 'Bash'
                environment name: 'LANGUAGE', value: 'All'
            }
          }
            steps {
                 sh '''
                    cd ${WORKSPACE}/scripts/
                    ./bashscript.sh >> results
                  '''
            }
        }
    }
    post {
            always {
                echo 'Saving Results process..'
                sh '''
                   report_file="${HOME}/Documents/Deployment/report"
                   mkdir -p ${HOME}/Documents/Deployment/
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


