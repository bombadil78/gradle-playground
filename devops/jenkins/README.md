# Create image
* cd jenkins
* sudo docker build -t my-jenkins .

# Run container (DooD)
* sudo docker run --name my-jenkins --restart unless-stopped -p 9999:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock -d my-jenkins