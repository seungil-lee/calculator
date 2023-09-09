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
		        	reportDir: "reports",
		        	reportFiles: "index.html",
		        	reportName: "JaCoCo Report"  
		        ])
		        sh "./gradlew jacocoTestCoverageVerification"
		    }
		}

	}
}