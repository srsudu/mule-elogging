# Mule Enterprise Logging

## The problem

Root cause analysis is one of the most important tasks in any mule project, but can be quite difficult and time consuming 
to do, especially in API project because for various reasons which include:
- HTTP logging can be used but misses critical information like what URL is being called, forcing developers to constantly go refer to the code
- HTTP logging happens in a different thread, so a log correlation id cannot be used
- APIKit wipes out the payload before the exception handling code receives it, making it impossible to log the reason for the error if you're using APIKit exception handling

## Why not use mulesoft services [json-logger](https://github.com/mulesoft-consulting/json-logger)

That json logger has one major flaw, the json is built as the message itself, and then when recording the event only that
message is logged. This has the significant downside of all logs generated by anything other that the json logger (ie. from
mule runtime framework, from other connectors) losing all metadata other than the message itself.

Also the logger itself isn't available as a scope, which makes it harder to properly record responses in error scenarios

Additionally this connector is designed to never cause the flow to fail, unlike json-logger which can cause various problems.

## The solution

This framework is designed to solve all those issues (and more) by providing the following capabilities:

1) logging payload and all metadata for all inbound/outbound operations (even when an exception occurs)
2) Record timings for inbound and outbound operations, allowing to quickly and easily identify time spend waiting for backend systems and time mule spent processing

# Reporting Issues

You can report new issues at this link http://github.com/Kloudtek/mule-elogging/issues.

# Licensing

Mule ELogging is licensed under the GPL 3
