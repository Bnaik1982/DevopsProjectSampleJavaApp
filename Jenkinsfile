pipeline {
    agent any 
    stages {
       stage('compile') {
	   steps {
                echo 'compiling..'
		   echo 'compiling again and again'
				git url: 'https://github.com/bnaik1982/DevopsProjectSampleJavaApp.git'
				sh script: '/opt/maven/bin/mvn compile'
           }
        }
       stage('codereview-pmd') {
	   steps {
                echo 'codereview..'
		   echo 'codereview again and again'
				sh script: '/opt/maven/bin/mvn -P metrics pmd:pmd'
           }
		post {
               success {
					recordIssues enabledForFailure: true, tool: pmdParser(pattern: '**/target/pmd.xml')
               }
           }		
        }
        stage('unit-test') {
		steps {
                echo 'unittest..'
	        sh script: '/opt/maven/bin/mvn test'
                 }
	   post {
               success {
                   junit 'target/surefire-reports/*.xml'
               }
           }			
        }
        stage('codecoverage') {
	   steps {
                echo 'unittest..'
		    echo 'codecoverage again and again'
	        sh script: '/opt/maven/bin/mvn verify'
                 }
	   post {
               success {
                   jacoco buildOverBuild: true, deltaBranchCoverage: '20', deltaClassCoverage: '20', deltaComplexityCoverage: '20', deltaInstructionCoverage: '20', deltaLineCoverage: '20', deltaMethodCoverage: '20'
               }
           }			
        }
        stage('package') {
	   steps {
                echo 'package......'
				sh script: '/opt/maven/bin/mvn package'	
           }		
        }
    }
}
