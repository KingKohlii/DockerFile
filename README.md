# DockerFile

What is Docker ?
> Docker is a software platform that allows you to build, test, and deploy applications quickly.
  Docker packages software into standardized units called containers
  Using Docker, you can quickly deploy and scale applications into any environment.

Why Use Docker?

1. Portability Across Machines
You may deploy your containerized program to any other system that runs Docker after testing it.
We can take image of conatiner and give it ahead for testing, here comes portability.

2.Isolation
Each Docker container is isolated,seperated from each others.
so if error occurs in any container it doesn't affect others, beacuse every container is isolated, unlike Virtual machine.

3.Rapid Performance
Container quickly booted up as it dont have O.S. as it have software servers.
But in V.M. diff. servers shares same O.S. and due to it take few min. to booted up, this is where containers better than V.M.

4.Container reuse
like templates, existing containers can be used as base images—essentially for building new containers.

5.Simplified Dependency Management
Eg.If one of your projects requires SQL and another project requires MariaDB
   Then you must uninstall one to get started with the other.It proves hassling and renders the project unusable.

   So Docker is here for the rescue! It provides a dependency management mechanism,
   Where each project or app can be isolated with all its dependencies in a separate container.
   Additionally, you can run multiple apps (containers) at a same time on the same machine.

* DockerFile - To create a Docker image, we have to provide a set of instructions that will build it.
             These instructions are provided with a Dockerfile.

1. Command FROM sets the base image to use.
2. WORKDIR command sets the working directory inside the image.
   If the directory does not exist, it will be created; this will be the location of our application.
3. RUN command- To install reuired dependencies.
4. CMD command specifies the command that runs when the container is started.
5. COPY . . to copy all resources from the current directory on the host computer to the working directory (/app) in the image.


* Dockerlize a Python Flask Application

We will show, how to do write a docker file for a flask application and run a container for Flask.
Github link — https://github.com/bikramatmedium/docker/tree/main/Dockerfile/python

1. Create a server.py flask file

from flask import Flask
#importing the flask class
app = Flask(__name__)
#creating an instance of the Flask class)

@app.route('/')
#The primary url for our application)
def hello_world():
#This method returns Flask Dockerized)
    return 'Flask Dockerized'

if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0')
#This statement starts the server on your local machine.)

2. Create requirements.txt file

click==8.0.1
colorama==0.4.4
Flask==2.0.1
itsdangerous==2.0.1
Jinja2==3.0.1
MarkupSafe==2.0.1
Werkzeug==2.0.1

3. Create a Dockerfile that contains instructions to build the flask application.

# Base Image
FROM python:3.8
# Working directory inside app
WORKDIR /app
#Copy the index.html file /usr/share/nginx/html/
COPY . /app
# Install app dependecy
RUN pip install -r requirements.txt
#Expose Nginx Port
EXPOSE 5000
#Start NginxService
ENTRYPOINT ["python"]
CMD ["app.py"]

Now we have three files dockerfile, app.py, and requirement.txt files.

Create Docker Image now
$ docker build -t flask-app .


4. Create a Container with the docker image created.
$ docker run -d -p 5000:5000 --name flask-app flask-app

An explanation of this command is as below
•       docker run is used for creating a docker container.
•       -d option is used to run a container in the background and print container ID.
•       -p option is used for port mapping between container and Host machine.
•       — name option is used to assign a name to the container.
•       In the end, we provide the name of the docker image from which we wish to run our container.

This will start the Python flask app on port 5000. If you visit http://ip:5000 in your browser.
