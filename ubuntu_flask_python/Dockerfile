FROM ubuntu:latest

RUN apt-get update && apt-get install -y --install-recommends \
                git \
		python \
                python-dev \
                python-setuptools \
		curl \
	&& rm -rf /var/lib/apt/lists/*

ENV HOME /home/user
RUN useradd --create-home --home-dir $HOME user \
        && chown -R user:user $HOME

ENV LANG C.UTF-8

RUN easy_install pip

WORKDIR $HOME

RUN git clone https://github.com/erikbeebe/sample_flask_mongodb_docker $HOME/sample_flask_mongodb_docker

RUN pip install -r sample_flask_mongodb_docker/requirements.txt

WORKDIR $HOME/sample_flask_mongodb_docker

EXPOSE 8080

USER user
CMD ["gunicorn", "app:app", "-w", "8", "-b", "0.0.0.0:8080"]
