# DockerJenkinsWithGitData

Dockerfile as the basis for a [data-container](https://docs.docker.com/userguide/dockervolumes/) for Jenkins. 

Simply put, this ensures that /var/jenkins_home exists and is owned by uid 1000 (the Jenkins user in the Jenkins image).

## Usage
You need to create a container prior to use.

```bash
docker run -name data-jenkins data-jenkins
```

And then you can run the Jenkins image, using the data-jenkins container as the data volume.

```bash
docker run -rm -p 8080:8080 -p 50000:50000 -volumes-from data-jenkins andrewgortonuk/dockerjenkinswithgit
```

Warning: If you delete the data-jenkins container (eg via docker rm data-jenkins), then you'll lose your data!

Use something like:-

```bash
docker ps -a | tail -n +2 | grep -v 'data-.*$'
```

to return you a list of all images which aren't named "data-*" which you could remove.

## Backup

```bash
mkdir -p backup
docker run --rm -volumes-from data-jenkins -v $(pwd)/backup:/backup ubuntu tar cvf /backup/backup.tar /var/jenkins_home
```

Note that centos:latest doesn't come with tar, and tar cvfZ will complain of broken pipes too.







