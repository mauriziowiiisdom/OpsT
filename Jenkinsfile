// this file must be present in the GitHub repository for Jenkins to be able to use it
node {
	try {
		// checks out remote repo to specified folder
		stage('Retrieve Repository') {
			dir('C:/GitHubReposServer/OpsT') {
				echo("***** Checking out repository *****")
				checkout scm
			}
		}
		stage('Run Wiiisdom Ops for Tableau Tests') {
			// Run Kinesis CLI as a shell command
			echo("***** Running tests *****")
			bat('"C:/Wiiisdom-Ops-for-Tableau-bundle-2023.4-win32/kinesis-cli/kinesis.bat" --canvas-timeout=240 --path "C:/GitHubReposServer/OpsT/Mau_Demo/test/Demo2Win" --output "C:/GitHubReposServer/OpsT/Reports" --context-vars "C:/GitHubReposServer/OpsT/Mau_Demo/context/prod.json" --recursive')
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
        bat('"C:/GitHubReposServer/S3_Upload.bat"')
		echo ("***** Job completed *****")
	}
}