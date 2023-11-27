node {
	try {
		stage('SCM Checkout') {
			echo("***** Checkout - file in repository folder *****")
			checkout scm
		}
		stage('Tableau Test (Wiiisdom Ops for Tableau)') {
			// Run Kinesis CLI as a shell command
			echo("***** Running test *****")
			bat('"C:/Wiiisdom-Ops-for-Tableau-bundle-2023.4-win32/kinesis-cli/kinesis.bat" --canvas-timeout=240 --path "C:/OpsT_Projects/Mau_Demo/test/Demo2Win" --output "C:/GitHubRepos/360Eyes-for-SAP-Data-Services/OpsTableau/Reports" --context-vars "C:/OpsT_Projects/Mau_Demo/context/prod.json" --recursive')
		}
	} catch (e) {
		echo("***** Job failed - check logs *****")
		throw(e);
	} finally {
		archiveReports();
	}
}

def archiveReports() {
	stage('Archive Test Evidences (Wiiisdom Ops for Tableau)') {
		echo("***** Job successful - archiving reports *****")
		archiveArtifacts artifacts: '**/report-*/'
	}
}