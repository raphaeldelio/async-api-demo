# AsyncAPI Demo
AsyncAPI is a specification for documenting message-driven APIs. It's based on OpenAPI.

In this demo, I try to configure AsyncAPI to work with Avro files. Even though I was able to do it with avsc files. 
I wasn't able to do it with avdl files.

There's also no integrated tool to generate messages to Kafka using the provided UI.

## Workflow
1. Define your Avro schema (.avsc files)
2. Define your AsyncAPI document with references to your Avro files
3. Generate documentation with the AsyncAPI Docker Generator:
```
docker run --rm -it \
-v ${PWD}/src/main/resources/asyncapi-definition.yml:/app/asyncapi.yml \
-v ${PWD}/output:/app/output \
-v ${PWD}/src/main/resources/avro:/app/avro \
asyncapi/generator -o /app/output /app/asyncapi.yml @asyncapi/html-template --force-write
```

## Key Takeaways
- We can define the documentation without the need to implement any line of code
- The documentation is generated as a static website. It has to be opened locally or hosted somewhere. If hosted, we
    need to configure implement and maintain pipelines to generate and deploy the documentation.
- The UI can not be used to generate messages to Kafka. 
- The yaml file cannot be opened through AsyncAPI Studio because it won't reference the Avro files correctly.
- The documentation may not reflect the latest documentation if developer forget to update it.
- It doesn't work with AVDL files.