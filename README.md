---

## DevOps Lab 6 – Containerization using Docker  
[https://github.com/ShriRadhey-Mishra/Lab_8.git]

Docker is a platform that allows us to automate the deployment of applications inside lightweight, portable containers. These containers package an application along with all its dependencies, making it easy to run the application in any environment without worrying about system compatibility issues.

In this lab, we built a Dockerfile to containerize a Python application that uses FastAPI. By doing this, we ensured that the application can be run consistently on any system that supports Docker.

Dockerfile Breakdown:
- `FROM ubuntu`: Defines the base image to be used, which in this case is Ubuntu.  
- `RUN apt update -y`: Updates the package list inside the container.  
- `RUN apt install python3 python3-pip pipenv -y`: Installs Python, pip, and pipenv to manage Python environments and dependencies.  
- `WORKDIR /app`: Sets the working directory inside the container to /app.  
- `COPY . /app/`: Copies all the files from the current directory to the container’s working directory.  
- `RUN pipenv install -r requirements.txt`: Installs all the required dependencies specified in the `requirements.txt` file.  
- `EXPOSE 80`: Indicates that the application will listen on port 80 inside the container.  
- `CMD pipenv run python3 ./main.py`: Defines the default command to run the FastAPI application when the container starts.

Using Docker in this lab helped us to package the Python + FastAPI application into a container image, which can be shared, deployed, and run anywhere with consistent results.

---

## DevOps Lab 7 – Build using GitHub Actions  
[https://github.com/ShriRadhey-Mishra/Lab_8.git]

In this lab, we took the file content from the last lab and we automated its build process using GitHub Actions. GitHub Actions is a Continuous Integration and Continuous Deployment (CI/CD) tool that allows us to automate workflows directly from our GitHub repository. Using GitHub Actions, we can automate the process of building, testing, and deploying our applications whenever we push code changes to our repository.

In this lab, we created a GitHub Actions workflow to automate the build process of our Dockerized FastAPI Python application. This ensured that our application’s Docker image gets built and pushed to Docker Hub automatically on every push to the repository.

Workflow breakdown:

- `name: docker image build`: Defines the name of the workflow.  
- `on: push`: Triggers the workflow to run every time a push is made to the repository.  
- `jobs: build`: Defines a job named build which contains the steps to be executed.  
- `runs-on: ubuntu-latest`: Specifies the environment where the job will run.  
- `steps`: Contains a sequence of actions to perform in this job.  
  - `uses: actions/checkout@v3`: Checks out the source code from the repository.  
  - `Check if secret is present`: Checks if the Docker token secret is available in GitHub secrets.  
  - `Log in to Docker Hub`: Logs into Docker Hub using the provided username and secret token.  
  - `Build Docker image`: Builds the Docker image from the Dockerfile in the repository using the command `docker build`.  
  - `Push Docker image`: Pushes the built Docker image to the specified Docker Hub repository.

Using this GitHub Actions workflow, we automated the build and deployment of our FastAPI Docker application, making our development and deployment process faster, more reliable, and efficient.

---
