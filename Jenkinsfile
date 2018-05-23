pipeline {
    agent any
    stages {
        stage('Git clone') {
            steps {
              checkout scm
            }
        }
        stage('Download S3 file') {
            steps {
                sh 'aws s3 cp s3://oldmutual-oracle-http-server/fmw_12.2.1.2.0_ohs_linux64_Disk1_1of1.zip OracleHTTPServer/dockerfiles/12.2.1.2.0/'
            }
        }
        stage('Run script') {
            steps {
              sh './OracleHTTPServer/dockerfiles/buildDockerImage.sh -v 12.2.1.2.0'
            }
        }
        stage('retag image and push') {
          steps {
            sh 'docker tag oracle/ohs:12.2.1.2.0-sa 068764521548.dkr.ecr.eu-west-1.amazonaws.com/oracle-http-server:12.2.1.2.0-sa'
            sh 'docker push 068764521548.dkr.ecr.eu-west-1.amazonaws.com/oracle-http-server:12.2.1.2.0-sa'
          }
        }
    }
}
