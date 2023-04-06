# Parodos Config Server Sample

The default implementation of the server storage backend uses git, so it easily supports labelled versions of configuration environments as well as being accessible to a wide range of tooling for managing the content.
It is easy to add alternative implementations and plug them in with Spring configuration.
The mini-application’s Environment is used to enumerate property sources and publish them at a JSON endpoint.

The HTTP service has resources in the following form:

/{app}/{profile}[/{label}]
/{app}-{profile}.yml
/{label}/{app}-{profile}.yml
/{app}-{profile}.properties
/{label}/{app}-{profile}.properties

where `app` is injected as the spring.config.name in the SpringApplication (what is normally application in a regular Spring Boot app), `profile` is an active profile (or comma-separated list of properties), and `label` is an optional git label (defaults to master.)

## Resources

| Path             | Description  |
|------------------|--------------|
| /{app}/{profile} | Configuration data for app in Spring profile (comma-separated).|
| /{app}/{profile}/{label} | Add a git label |
| /{app}/{profile}{label}/{path} | An environment-specific plain text config file (at "path") |
| /{app}-{profile}.yml | Active profiles take precedence over defaults, and, if there are multiple profiles, the last one wins (similar to adding entries to a Map). |
| /{label}/{app}-{profile}.yml | `label` which is a server side feature labelling a "versioned" set of config files. |
| /{app}-{profile}.properties | similar as above in properties format | 
| /{label}/{app}-{profile}.properties | similar as above in properties format | 

## Security

The server is not secure by default. You can add HTTP Basic
authentication by including an extra dependency on Spring Security
(e.g. via `spring-boot-starter-security`).
