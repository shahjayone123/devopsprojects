node{
	stage('SCM Checkout'){
		git branch: 'wartomcat', url: 'https://github.com/shahjayone123/devopsprojects.git'
	}
	stage('Compile-Package'){
		def mvnHome = tool name: 'maven-3.5.4', type: 'maven'
		sh "${mvnHome}/bin/mvn package"
	}
	stage('Deploy to Tomcat'){
		sshagent(['tomcat-server']) {
		sh 'scp -o StrictHostKeyChecking=no target/*.war ec2-user@http://3.16.109.110:/opt/tomcat9/webapps/'
	}
	}	
}
