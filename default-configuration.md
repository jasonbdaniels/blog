[toc]

---

# Configuration File
The news apps utilize a *default-configuration.json* file which provides the app with supported features, behavior, and functionality. The configuration file is accessed on a remote server and is requested on every app launch. To prevent unnecessary data downloads, the configuration is first requested with the HTTP HEAD method. Upon response the HTTP Header etag is inspected for a non-matching value. If the value is different then the configuration file is requested with the HTTP GET method.

# Network Communication Diagrams
## Non-Matching eTag
```sequence
App->Server: HEAD: default-configuration.json
Server-->App: eTag: 0123456789 ...
note left of App: If eTag is different from\n previous requests?\n GET the configuration file
App->Server: GET: default-configuration.json
Server-->App: default-configuration.json[bytes]
note left of App: Save configuration file and\n it's eTag.
```

## Matching eTag
```sequence
App->Server: HEAD: default-configuration.json
Server-->App: eTag: 0123456789 ...
note left of App: eTag matches the current\n configuration file.\n Communication finished.
```