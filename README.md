## ElasticSearch Dockerfile


This repository contains **Dockerfile** of [ElasticSearch](http://www.elasticsearch.org/) for [Docker](https://www.docker.io/)'s [trusted build](https://index.docker.io/u/dockerfile/elasticsearch/) published to the public [Docker Registry](https://index.docker.io/).


### Dependencies

* [dockerfile/java](http://dockerfile.github.io/#/java)


### Installation

1. Install [Docker](https://www.docker.io/).

2. Build an image from Dockerfile: `docker build -t="jbasdf/elasticsearch" github.com/jbasdf/elasticsearch`)


### Usage

    docker run -d -p 9200:9200 -p 9300:9300 jbasdf/elasticsearch

#### Attach persistent/shared directories

  1. Create a mountable data directory `<data-dir>` on the host.

  2. Create ElasticSearch config file at `<data-dir>/elasticsearch.yml`.

    ```yml
    path:
      logs: /data/log
      data: /data/data
    ```

  3. Start a container by mounting data directory and specifying the custom configuration file:

    ```sh
    docker run -d -p 9200:9200 -p 9300:9300 -v <data-dir>:/data dockerfile/elasticsearch -Des.config=/data/elasticsearch.yml
    ```

    Or run a named container without specifying ports if you are using nginx_es:
    ```
    docker run -d --name elasticsearch -v /data:/data dockerfile/elasticsearch
    ```

Open `http://<host>:9200` to see the result.


### Troubleshooting:

If you see this error:
  Error: Conflict, The name elasticsearch is already assigned to 98edd9bdd309. You have to delete (or rename) that container to be able to assign elasticsearch to a container again.

Be sure to remove the container before calling docker run:
  docker rm elasticsearch