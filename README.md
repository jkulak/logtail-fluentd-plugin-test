# Intro

When using `logtail` `fluentd` plugin: <https://docs.logtail.com/log-forwarding/fluentd> only some logs are saved/sent to Logtail.

Below images show console output, and what is being logged in Logtail. It's every third, sometimes, every second, sometimes every fifth, I see no rule.

For testing purposes I have created an alternative config, where `fluentd` saves data to file, stdout and sends to Logtail, and again, Logtail is missing most of the events.

![iTerm2 output](https://raw.githubusercontent.com/jkulak/logtail-fluentd-plugin-test/media/iterm.png)

![Logtail view](https://raw.githubusercontent.com/jkulak/logtail-fluentd-plugin-test/media/logtail.png)

## Test

1. `docker build -t fluentd-server .` - build fluentd image (official)
1. `docker run -ti --rm -p 24224:24224 -v $(pwd)/etc:/fluentd/etc fluentd-server` - run fluentd container
1. `docker run -it --rm --log-driver=fluentd alpine ping 127.0.0.1` - Run container with logging

Config file `etc/fluent.conf` has two suggested by Logtail configurations, one from the website, when adding the source, and the other from the GitHub README.md.

## Alternative config file

Alternative config file, sends logs to different outputs, which show, that `stdout` and a log file get all the events and Logtail receives only some.

Use `docker run -ti --rm -p 8888:8888 -p 24224:24224 -v $(pwd)/etc:/fluentd/etc -v $(pwd)/log:/var/log/fluent/ fluentd-server` to run the container for alternative config.
