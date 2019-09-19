# stack-docker

This example Docker Compose configuration demonstrates many components of the
Elastic Stack, all running on a single machine under Docker.

## Prerequisites

- Docker and Docker Compose.
- At least 4GiB of RAM for the containers. Windows and Mac users _must_
configure their Docker virtual machine to have more than the default 2 GiB of
RAM.
- Linux Users must set the following configuration as `root`:

```sh
sysctl -w vm.max_map_count=262144
```

By default, the amount of Virtual Memory [is not enough](https://www.elastic.co/guide/en/elasticsearch/reference/current/vm-max-map-count.html).

## Starting the stack

First we need to:

1. set default password
2. Create SSL certs
3. create keystores to store passwords
4. install dashboards, index patterns, etc.. for beats and apm

This is accomplished using the setup.sh script:

```sh
./setup.sh
```

Please take note after the setup completes it will output the password
that is used for the `elastic` login.

Now we can launch the stack with `docker-compose up -d` to create a demonstration Elastic Stack with
Elasticsearch, Kibana, Logstash, Metricbeat and Filebeat.

Point a browser at [`http://localhost:5601`](http://localhost:5601) to see the results.
> *NOTE*: Elasticsearch is now setup with self-signed certs.
> This means anytime you want to interact with elasticsearch by using other tools/clients you must use
> https, and if you want to get the `ca.crt` you can get it by running
> `docker exec -it elasticsearch cat /usr/share/elasticsearch/config/certs/ssl/ca/ca.crt`

Log in with `elastic` and what ever your auto generated elastic password is from the
setup.
