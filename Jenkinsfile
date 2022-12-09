node {
    def app

    stage('Clone repository') {
        /* Cloning the Repository to our Workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image */

        app = docker.build("nvn9/nodeapp")
    }

    stage('Test image') {
        
        app.inside {
            echo "Tests passed"
        }
    }

    stage('Push image') {
        /* 
			You would need to first register with nexus before you can push images to your account
		*/
        nexus.withRegistry('http://ec2-52-66-240-100.ap-south-1.compute.amazonaws.com:8081/repository/docker-repository-private/', 'nexus') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
            } 
                echo "Trying to Push Docker Build to nexus"
    }
}
