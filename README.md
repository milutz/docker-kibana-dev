# Docker Kibana Development

![](https://images.microbadger.com/badges/image/rigon/kibana-dev.svg)

Docker image with Kibana for plugin developement


## How to run

This image requires an [elasticsearch](https://hub.docker.com/_/elasticsearch/) up and running with the same version of Kibana:

    $ docker run --name some-elasticsearch -p 9200:9200 -d docker.elastic.co/elasticsearch/elasticsearch:[version]

This image includes EXPOSE 5601 (default port). If you'd like to be able to access the instance from the host without the container's IP, standard port mappings can be used:

    $ docker run --name some-kibana --link some-elasticsearch:elasticsearch -p 5601:5601 -t rigon/kibana-dev

If you are developing a plugins for Kibana, you might want to mount the plugins folder in Kibana with a volume:

    $ docker run --name some-kibana -v plugins_folder:/kibana/plugins:rw --link some-elasticsearch:elasticsearch -p 5601:5601 -t rigon/kibana-dev

Or if you are only developing one plugin, you might want to mount the plugin folder directly into Kibana:

    $ docker run --name some-kibana -v plugin_path:/kibana/plugins/plugin_name:rw --link some-elasticsearch:elasticsearch -p 5601:5601 -t rigon/kibana-dev
