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
	} catch (e) {
		echo("***** Job failed - check logs *****")
		throw(e);
	} 
	finally {
		archiveTestResults();		
	}
}

def archiveTestResults(){
	stage('Archive Test Evidence to S3 bucket'){
		echo("***** Archiving reports to S3 bucket *****")
        bat('"C:/GitHubRepos/S3_Upload.bat"')
		echo ("***** Job completed *****")
	}
}