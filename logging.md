# Logging

We need to see how the production system is working, so we know if there are any errors, and to better understand how it works in a live system in order to improve it.  For this end, there are two separate topics - logging and metrics.

Logging is the process of writing information that happens to the system to another source.  This could be as simple as the http request log written to the file, so we know which endpoints were called when.  Or writing stack traces to a third party system (eg. bugsnag, sentry), so we can do a full post-mortem on any errors.

Metrics (for me) is monitoring numeric system values, such as response time, load, etc.  We can graph this in eg. grafana and also trigger alarms when these reach min/max values. This is just what AWS Cloudwatch does.

Here we will just discuss the logging issue.

## Requirements

First off, we have different logging requirements in production, staging, and development, so it should be something easily configurable.  And we will want to write different information to different services, best in a machine readable format (eg json) to allow for future post-processing.  

For example, in development, I want to:
  * print full stack trace on any exception to stderr
  * print http request log to stdout
  * print debug sql statements to stdout if a --verbose flag is passed on the command-line
 In production, I want to:
  * send any unhandled panics to bugsnag
  * send all http request logs to logstash
  * send sql statements taking over 10ms to logstash
  * send slack notification on any request taking over 1 minute

I don't want to put this logic all over the code to look at the environment and select the loggers and destinations.  Better if we have one logger than can do this, and just call something like:

```
logger.Error(err)
logger.Info('http', path, timestamp, ip, response_time)
logger.Debug('sql', statement, query_time)
```

## Logrus

One top contender for this area is https://github.com/Sirupsen/logrus, which does some nice handling of json fields, and configuring multiple hooks for output ( https://github.com/Sirupsen/logrus#hooks ).  You can also pair it with a nice utility https://github.com/gogap/logrus_mate to configure the logging for multiple environments in a config file.

It seems quite easy to add a hook, that can be added to all logging, without adding the api call everywhere in the code. For example https://github.com/Shopify/logrus-bugsnag/blob/master/bugsnag.go  And if you want, you can allow the hook to specify which levels it responds to: https://github.com/johntdyer/slackrus#use

Will write more when I have some hands-on experience.