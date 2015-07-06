# docker-ci - Docker Continuous Integration Framework
Docker-compose to provision a complete Continuous Integration Framework (CI). The following products are configured as part of the framework:

- Gitlab (http://192.168.59.103:10080): https://github.com/sameersbn/docker-gitlab
- Jenkins (http://192.168.59.103:32768): https://github.com/jenkinsci/docker
- SonarQube (http://192.168.59.103:49000): https://github.com/SonarSource/docker-sonarqube
- Artifactory (http://192.168.59.103:38081): https://www.jfrog.com/confluence/display/RTF/Docker+Repositories
- Docker Private Registry (http://192.168.59.103:5000): https://docs.docker.com/registry/deploying

The main goal of this compose is to provide a tool to quickly set up a CI environment. It is intended for those who want to start researching about CI and do some testing using the above products. You can easily run the full stack on one VM.

The basic flow is as follows:

1. The developers push changes to a Gitlab repo which is configured with a web-hook pointing to a Jenkins job.
2. Once the web-hook is triggered, Jenkins starts executing the job. The job will download the Gitlab repo, compile, test, analysis (SonarQube), package and deploy it to Artifactory.
3. Once deployed, Jenkins can build a Docker image and commit it to the registry.
4. Finally, Jenkins can invoke a shell script to run a docker image with the generated artefact. 

# Get Started
First you will need to edit `docker-compose.yml` to set the shared folders where the products will store the persistence data.
After that, you just need to execute `docker-compose up` (in the same folder where you downloaded this repository).
