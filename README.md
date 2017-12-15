# Steps to get up and running
## Install Docker and add user
``` shell
$ sudo apt install docker.io docker-compose -y
$ sudo usermod -aG docker $USER
```
## Create the folder structure
``` shell
~/anaconda3_docker$ tree
.
├── data
├── docker-compose.yml
├── Dockerfile
├── notebooks
├── README.md
└── requirements.txt
```
The data folder will contain input and output data for the notebooks. The notebooks folder will contain the Jupyter notebooks. The Dockerfile will create the folders in the container and install the Python requirements from the requirements.txt.

Content of Dockerfile:
```
FROM continuumio/anaconda3
ADD requirements.txt /
RUN pip install -r requirements.txt
CMD ["/opt/conda/bin/jupyter", "notebook", "--notebook-dir=/opt/notebooks", "--ip='*'", "--no-browser", "--allow-root","--port=8558"]
```

Content of docker-compose.yml:
```
version: '2'
services:
  anaconda:
    build: .
    volumes:
      - ./notebooks:/opt/notebooks
    ports:
      - "8558:8558"

```

## Start the container
``` shell
~/anaconda3_docker$ docker-compose up --build
```

## Action
Go to your IP-address on the given port and start coding.