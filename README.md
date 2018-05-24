# Splunk + fluent-bit integration via HEC

This docker-compose image uses,

 - [A public, official splunk enterprise image](https://hub.docker.com/r/splunk/splunk/)
 - [A public, official splunk enterprise universalforwarder image](https://hub.docker.com/r/splunk/universalforwarder/)
 - [A public, official fluentbit image](https://hub.docker.com/r/fluent/fluent-bit/)

Bring up the containers by running,

    docker-compose build
    docker-compose up

To bring down and clean up the containers run `docker-compose down`

## Functionality

This composition configures fluent-bit to read out memory and CPU metrics,
transform them and send them to Splunk via the HTTP Event Collector (HEC). The
main Splunk instance contains an example dashboard displaying the incoming
metrics.

## UI   

| Function       | URL                                              | Username  | Password |
|----------------|--------------------------------------------------|-----------|----------|
| Splunk UI      | [http://localhost:8000/](http://localhost:8000/) | admin     | admin    |


## Composition

![fluent-bit Splunk HEC](/resource/splunk-fluentbit-components.png?raw=true "fluent-bit Splunk HEC")

The Splunk HF, IDX and SHC components are all run by the main `splunk` image.

## Pipeline - fluent-bit

![fluent-bit pipeline](/resource/fluent-bit-pipeline.png?raw=true "fluent-bit pipeline")

Main [`fluent-bit.conf`](/volumes/fluent-bit-etc/fluent-bit.conf)

## Shell

For a shell on the containers, run the commands below.

    ./script/shell-splunk.sh
    ./script/shell-splunkforwarder.sh
    ./script/shell-fluentbit.sh

## Testing

    curl -u 'x:3e6ffd12-0f69-46bb-ad0d-71cffb661a0d' -X POST -d'{"event":"xxx"}' http://localhost:8088/services/collector/event

