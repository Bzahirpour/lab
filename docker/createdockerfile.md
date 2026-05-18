A docker file always starts with FROM <base_image>
Alpine is small around 5-7 mb, but you can use ubuntu
or debian also.

Then we can use RUN for the commands necessary to set
up the env, like installing software, updating packages
or creating files. You can get this by setting it up
locally and then looking at the command history.

COPY can be used to pass the source code into the 
container

ENTRYPOINT sets the default exe command that runs
everytime the container starts from the image.
if you add ENTRYPOINT sleep to the dockerfile
then when you docker run <image> 10 it will run sleep 10
(command parameter gets appened instead of replaced like with CMD)
can be overwritten with the --entrypoint flag

CMD sets an additional cmd to run. (if no ENTRYPOINT it becomes the default cmd)
CMD command param1 or ["command", "param1"]
CMD sleep 5 or ["sleep", "5"]

EXAMPLE
```dockerfile
FROM ubuntu

RUN apt-get update
RUN apt-get install -y python python-pip
RUN pip install flask

COPY app.py /opt/app.py

ENTRYPOINT FLASK_APP=/opt/app.py flask run --host=0.0.0.0
```

BY DEFAULT will sleep for 5 unless you docker run <image> 10 then the 5 will be overwritten
```dockerfile
ENTRYPOINT sleep

CMD 5
```
Then we use:
docker build . -t <account/tag>

It will then be available as an image

docker push <account/tag>
(after docker login)
