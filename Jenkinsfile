pipeline {
    agent any
    tools {
        maven "MAVEN3"
        jdk "OracleJDK"
    }

    environment {
    SNAP_REPO           = 'vprofile-snapshot'
	NEXUS_USER          = 'admin'
	NEXUS_PASS          = 'Kamji123'
	RELEASE_REPO        = 'vprofile-release'
	CENTRAL_REPO        = 'vpro-maven-central'
	NEXUSIP             = '172.31.30.157'
	NEXUSPORT           = '8081'
	NEXUS_GRP_REPO      = 'vpro-maven-group'
    NEXUS_LOGIN         = 'nexuslogin'
        

    }

    stages {
        stage('Build'){
            steps {
                sh 'mvn -s settings.xml -DskipTests install'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage('UNIT TEST'){
            steps {
                sh 'mvn test'
            }
        }

        stage('INTEGRATION TEST'){
            steps {
                sh 'mvn verify -DskipUnitTests'
            }
        }
        stage ('CODE ANALYSIS WITH CHECKSTYLE'){
            steps {
                sh 'mvn checkstyle:checkstyle'
            }
            post {
                success {
                    echo 'Generated Analysis Result'
                }
            }
        }

    }
}
