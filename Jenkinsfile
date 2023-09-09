pipeline {
	agent any
	stages {
		stage("Compile") {
			steps {
				sh "chmod +x gradlew"
				sh "./gradlew compileJava"
			}
		}
		stage("Unit Test") {
			steps {
				sh "./gradlew test"
			}
		}
		stage("Code coverage"){
		    steps {
		        sh "./gradlew jacocoTestReport"
		        publishHTML (target: [
					allowMissing: false,
					alwaysLinkToLastBuild: true,
					keepAll: true,
		        	reportDir: "/var/jenkins_home/workspace/calculator/build/reports/jacoco/test/html",
		        	reportFiles: "index.html",
		        	reportName: "JaCoCo Report"  
		        ])
		        sh "./gradlew jacocoTestCoverageVerification"
		    }
		}
		stage("Static code analysis") {
			steps {
   		    	sh "./gradlew checkstyleMain"
   		    	publishHTML (target: [
					allowMissing: false,
					alwaysLinkToLastBuild: true,
					keepAll: true,
		        	reportDir: "/var/jenkins_home/workspace/calculator/build/reports/checkstyle/",
		        	reportFiles: "main.html",
		        	reportName: "Checkstyle Report"  
		        ])
   			}
		}
	}
}