# node-jenkins-docker

It is just a simple node.js app which doesn't really matter here. What matters is how it connects with the Jenkins pipelines as well as the Docker conteiner. 
In jenkins simply create a new pipeline job and use the `Pipeline script from SCM` option. Choose your repository and remember to create your credentials in Jenkins in order to connect to either private docker repo or docker hub (`Home -> Credentials -> click on global -> Add credentials`). For docker hub it may be: `Username and password ; Username: twlphaseii ; Password: xxxxxx ; ID: dockerhub` <-- you'll rely on this ID in Jenkinsfile.

By running this pipeline in Jenkins you will simply checkout the repo, build it and test it, tag the docker image and push it to docker hub.

### todo

- kubernetes integration
- consider node_modules