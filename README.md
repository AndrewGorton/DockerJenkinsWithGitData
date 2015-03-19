# DockerJenkinsWithGitData

Dockerfile as the basis for a [data-container](https://docs.docker.com/userguide/dockervolumes/) for Jenkins. 

Simply put, this ensures that /var/jenkins_home exists and is owned by uid 1000 (the Jenkins user in the Jenkins image).


