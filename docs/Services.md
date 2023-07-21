# Configuring a Service for Scanning
This document describes the configuration process and available methods for parsing a new service. Note that custom services may need a little bit of work to normalize the data.

## Service Definition Block
Here is an example service definition block to get you started; you can add this to `configs/services.yml`. In the future we will support importing .yml files from the services directory so you can add each service in its own file if you want.
```yaml
services:
    - service-name: my-service
        method: "arin-query"
        sources:
            - "ASXXXXX"
        status: "validated"
        types:
            - ipv4
        enabled: true
```

## When a new Definition is Needed
Right now, to simplify things, each method of parsing a service will need its own defintion. If you intend to parse something based of their ASN as well as Web page, you will need two service definitions for this. In the future I intend to enable a single definition per service that will rely on a prefix appended to the source to determine what method it should use.

##  Parsing Methods Supported/Planned
1. JSON/YML/Text Parsing
2. Web Scraping
3. Query ARIN or equal regional entity assignment database
4. WhoIs Query
5. REST API Calls (where available)
6. Simple Name Resolution (nslookup, etc)

### Configuring a Method
```yaml
services:
    - service-name: my-service
        method: <"arin-query" | "yml" | "json" | "txt" | "whois" | "web-scrape" | "rest" | "nslookup">
        // Omitted for brevity
```

## Sources
This supports an array of sources, meaning that you can parse multiple webpages, API methods, WhoIsEntries, Files, etc using one service definition. There is no limit to the number of sources you can parse for a single service definition.
1. WhoIs and Name Resolution should simply be the domain name, nothing else.
2. REST APIs will need additional configuration for authenticaiton where needed; this is planned and not currently supported
3. WhoIs won't produce lists useable for creating security rules, but can help you map out the service and point to where you might be able to obtain the information needed.
4. For IP Address Assignment, we're currently only querying ARIN, other regional authorities will be added later

### Configuring Sources
```yaml
services:
    - service-name: my-service
        // Omitted for brevity
        sources:
            - <"domain" | "url" | "ARIN-ASN" | "file-path">
```

## Status
Status is determined based on whether I have validated it to work properly. This will be automatically updated during build checks and regression testing based on the format of the output data. 
* Validated, a status of validated indicates that the parsing works as expected and is producing actionable and normalized output data
* Planned, a status of planned indicates that I have the approriate data needed to validate the service, but it hasn't yet been implemented completely
* Investingating - a status of investigating indicates that I still require additional information to be able to parse this service

## Types
Configuring types allows you to specify what data you expect to grab from a service. This is important as the script needs to know what data is it looking for. These are dictated by Regular Expressions, in the future we will support custom RegEx, but for now you can simply define it using a keyword. Currently supported types are IPv4 Addresses (public and non-public), IPv6 Addresses (all), URLs, and FQDNs.

### Configuring Types
```yaml
services:
    - service-name: my-service
        // Omitted for brevity
        types:
            - <"ipv4" | "ipv6" | "url" | "domain">
```

## Enabling a Service
Services are only scanned if they're enabled. To support this, a simple boolean check is added. To enable a service, simple set `enabled: false` to `enabled: true`


## Example Fully Configured Service
Simple place the scheme in the `configs/schemas/` directory and add the schema to the `configs/services.yml` file.

```yaml
services:
  - service-name: cisco-webex
    method: "web-scrape"
    sources: 
      - "https://help.webex.com/en-us/article/WBX000028782/Network-Requirements-for-Webex-Services"
    status: "validated"
    types:
      - ipv4
      - domain
    enabled: true
```
