node{
	stage('SCM Checkout'){
		git branch: 'slacknotification', url: 'https://github.com/shahjayone123/devopsprojects.git'
	}
	stage('Compile-Package'){
		def mvnHome = tool name: 'maven-3.5.4', type: 'maven'
		sh "${mvnHome}/bin/mvn package"
	}
	stage('Deploy to Tomcat'){
		sshagent(['tomcat-server']) {
		sh 'scp -o StrictHostKeyChecking=no target/*.war ec2-user@18.191.180.16:/opt/tomcat9/webapps/'
		}
	}
	stage('Email Notification'){
	mail bcc: '', body: 'This is body', cc: '', from: 'shahjayone@gmail.com', replyTo: 'shahjayone@gmail.com', subject: 'This is Subject', to: 'prabhat@aptence.com'
	}
	stage('Slack Notification'){
	slackSend baseUrl: 'https://hooks.slack.com/services/', channel: '#jenkins', color: '#439FE0', message: 'Jenkins new build added', teamDomain: 'intelycore03', tokenCredentialId: 'slack-secret'
	}

}
