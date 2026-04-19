# Quickstart

1. Grab elastic-local from https://github.com/elastic/start-local
	Run with ./start-local.sh
	Note the api key 
2. Grab the elastic-agent from https://www.elastic.co/downloads/elastic-agent
	Create otel config 
```
receivers:
  otlp:
   protocols:
     grpc:
exporters:
  # Exporter to send logs and metrics to Elasticsearch
  elasticsearch/otel:
    endpoints: [ "http://localhost:9200" ]
    api_key: <API Key from 1.>
    mapping:
      mode: otel
service:
  pipelines:
    logs/platformlogs:
      receivers: [otlp]
      exporters: [elasticsearch/otel]
```
 
3. Add the following to claude settings

```
  "env": {
    "OTEL_EXPORTER_OTLP_ENDPOINT": "http://localhost:4317",
    "OTEL_EXPORTER_OTLP_PROTOCOL": "grpc",
    "OTEL_LOGS_EXPORTER": "otlp",
    "OTEL_LOG_USER_PROMPTS": "1",
    "OTEL_LOG_TOOL_DETAILS": "1",
    "OTEL_LOG_TOOL_CONTENT": "1",
    "OTEL_LOG_RAW_API_BODIES": "1"
  }
```

4. Start otel collector
sudo ./otelcol --config otel.yml

5. Start Claude Code


