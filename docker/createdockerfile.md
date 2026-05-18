# A docker file always starts with FROM <base_image>
# Alpine is small around 5-7 mb, but you can use ubuntu
# or debian also.

# Then we can use RUN for the commands necessary to set
# up the env, like installing software, updating packages
# or creating files. You can get this by setting it up
# locally and then looking at the command history.

# COPY can be used to pass the source code into the 
# container

# ENTRYPOINT sets the default exe command that runs
# everytime the container starts from the image.


# EXAMPLE
```dockerfile
FROM ubuntu

RUN apt-get update
RUN apt-get install -y python python-pip
RUN pip install flask

COPY app.py /opt/app.py

ENTRYPOINT FLASK_APP=/opt/app.py flask run --host=0.0.0.0
```
