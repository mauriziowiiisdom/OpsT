// this file must be present in the GitHub repository for Jenkins to be able to use it
node {
	try {
		stage('SCM Checkout') {
			echo("***** Checking out repository *****")
			checkout scm
		}
		stage('Run Wiiisdom Ops for Tableau Test') {
			// Run Kinesis CLI as a shell command
			echo("***** Running test *****")
			bat('"C:/Wiiisdom-Ops-for-Tableau-bundle-2023.4-win32/kinesis-cli/kinesis.bat" --canvas-timeout=240 --path "C:/GitHubRepos/OpsT/Mau_Demo/test/Demo2Win" --output "C:/GitHubRepos/OpsT/Reports" --context-vars "C:/GitHubRepos/OpsT/Mau_Demo/context/prod.json" --recursive')
		}
		stage('Archiving artifacts to S3'){
			echo("***** Archiving reports to S3 bucket *****")
            bat('"C:/GitHubRepos/S3_Upload.bat"')
		}
	} catch (e) {
		echo("***** Job failed - check logs *****")
		throw(e);
	} 
	finally {
	//	archiveReports();
		archiveTestResults()		
	}
}

def archiveTestResults(){
	stage('Archive Test Evidence (Wiiisdom Ops for Tableau)'){
		echo("***** Archiving reports to S3 bucket *****")
        bat('"C:/GitHubRepos/S3_Upload.bat"')
		echo ("***** Job completed *****")
	}
}

//def archiveReports() {
//	stage('Archive Test Evidence (Wiiisdom Ops for Tableau)') {
//		echo("***** Job successful - archiving reports *****")
//		archiveArtifacts artifacts: 'Reports*/'
//	}
//}