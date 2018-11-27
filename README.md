# Knative Websocket EventSource

A simple, pluggable, websocket-based event source to be used in a Knative Eventing context.

## Usage

To create a source, reading from a given Websocket server, apply a YAML like the following:

```yaml
apiVersion: sources.eventing.knative.dev/v1alpha1
kind: ContainerSource
metadata:
  name: my-new-source
spec:
  image: github.com/markusthoemmes/knative-websocket-eventsource/cmd
  args:
    # mandatory: URL to connect to for events
    - '--source=wss://my.websocket.server/streaming'
    # optional (default: "websocket-event"): The type of event this will emit
    - '--eventType=my-nice-events'
    # option (default: source-url): The source where the events are coming from
    - '--eventSource=my.websocket.server'
  # Adjust this to the sink you want to point to
  sink:
    apiVersion: eventing.knative.dev/v1alpha1
    kind: Channel
    name: my-old-channel
```