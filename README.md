# docker_flask_homework

This assignment aims to provide hands-on experience in Dockerizing Flask applications, first individually and then using Docker Compose for managing multiple applications.


# Part One: Dockerizing a Single Flask Application
- Create a folder called Part1 and within this folder, create three files titled Dockerfile, app.py, and requirements.txt
- The <code>app.py</code> file will contain code for Flask app
- The purpose of the Dockerfile is to containerize the Flask application
- The following code was entered in the <code>Dockerfile</code>

```python
# pull a specific version of python from the docker hub
FROM python:3.10-slim-buster
# creating new virtual OS 
WORKDIR /app
# puts files in directory and places it in virtual OS
COPY . /app/
# installs requprements.txt file
RUN pip install -r requirements.txt
# exposes port 5000 to virtual OS to enable communication
EXPOSE 5000
# run command to run web application
CMD ["python", "app.py"]
```

- In the Google Shell Editor, open the terminal and cd into the Part1 folder.
- We will need to build a docker image using <code>docker build -t [your-image-name] . </code>
- Be sure to add the period at the end of this command!
- Enter <code>docker images</code> to view a list of existing images 
- To run the image, use <code>docker run -p [machine-port-number]:[docker-image-port-number] [your-image-name]</code>
- <code>docker ps</code> will display a list of the running containers 

# Part Two: Multi-Container Setup with Docker Compose

- Create a new <code>Part2</code> folder (make sure this is separate from Part1)
- Within the Part2 folder, create two distinct Flask applications: <code>Flask1</code> and <code>Flask2</code>
- You can use the above steps from Part One for building a Flask application with Docker 
- Make sure you are outside of the Part1 and Part2 folders, and create a <code>docker-complose.yml</code> file
- The <code>docker-complose.yml</code> file contains the following:

```python
# docker compose version 
version: '3'

# list of different containers in the application
services:

# first flask app
  flask_app_1:
    # directs the image being built to Flask1's dockerfile
    build: ./Flask1
    # uses port 5001 for host and 5000 for container 
    ports:
      - "5001:5000"
    # changes in local files will be brought to the application 
    volumes:
      - ./Flask1:/app
```

- Enter <code>docker-compose up --build </code> to dockerize 
- Note: it may take some time for the applications to be built
- To re-run the applications, use <code>docker-compose up</code>

# Differences in Docker Compose and Docker 
- Docker Compose allows the user to dockerize multiple applications using one file (docker-compose.yml). For Docker alone if there are multiple containers, the user will have to start and command each container separately.
      
