# kaggleToolBox


```Dockerfile
FROM gcr.io/kaggle-gpu-images/python:latest 

RUN pip install -U pip && \
    pip install black && \
    pip install jupyter-contrib-nbextensions && \
    jupyter contrib nbextension install && \
    jupyter nbextensions_configurator enable && \
    jupyter nbextension install https://github.com/drillan/jupyter-black/archive/master.zip && \
    jupyter nbextension enable jupyter-black-master/jupyter-black
```


```Dockerfile
version: "3"
services:
  kaggle-gpu-action:
    build: .
    # image: kaggle-gpu-action:v1
    volumes:
      # host側のmount元 path : docker側のmount先path
      - .:/home
    working_dir: /home
    ports:
      - 8686:8888
    #command: jupyter-lab --ip 0.0.0.0 --allow-root --NotebookApp.token='' --port=8888 --notebook-dir=/home -b localhost
    command: jupyter-lab --ip=0.0.0.0 --allow-root --no-browser --NotebookApp.token=''

    runtime: nvidia
```