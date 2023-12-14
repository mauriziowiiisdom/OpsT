// this file must be present in the GitHub repository for Jenkins to be able to use it
node {
	try {
		stage('SCM Checkout') {
			echo("***** Checking out repository *****")
			checkout scm
		}
		stage('Retrieve Repository') {
			// Copy last version of repository to OpsT server
			echo("***** Copying repository to OpsT server *****")
			bat('"C:/GitHubRepos - Server/retrieve_repo.bat"')
			echo ("***** Completed *****")
		}
		stage('Run Wiiisdom Ops for Tableau Tests') {
			// Run Kinesis CLI as a shell command
			echo("***** Running tests *****")
			bat('"C:/Wiiisdom-Ops-for-Tableau-bundle-2023.4-win32/kinesis-cli/kinesis.bat" --canvas-timeout=240 --path "C:/GitHubRepos - Server/OpsT/Mau_Demo/test/Demo2Win" --output "C:/GitHubRepos - Server/OpsT/Reports" --context-vars "C:/GitHubRepos - Server/OpsT/Mau_Demo/context/prod.json" --recursive')
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
        bat('"C:/GitHubRepos - Server/S3_Upload.bat"')
		echo ("***** Job completed *****")
	}
}