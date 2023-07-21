# Description
PyNetSecWatch is a simple Python tool that will allow you to parse webpages, WhoIs, ARIN, and other sources to generate complete lists of all known address and ports for a configured service. This is a smaller component of a project I'm working on that will parse for common services and create a REST API and Webpage users can use for a centralized list of all known service information and firewall rules that would be needed to allow, deny, or log traffic to a specific service. This is just a project to help me along my DevNet studies, obviously things like this already exist, but what fun is using something that exists when you can create your own?
create 

# Known Services
__This is a list of planned services. it is subject to change.__
- [ ] Amazon Prime Video
- [ ] Amazon Web Services
- [ ] BlueJeans
- [ ] Cisco Security Cloud
- [ ] Cisco Webex
- [ ] Dialpad
- [ ] Disney Plus
- [ ] Google Video
- [ ] Google Voice
- [ ] Hulu
- [ ] Microsoft 365 
- [ ] Microsoft Azure
- [ ] Netflix
- [ ] Pandora Radio
- [ ] Ring Central
- [ ] Skype
- [ ] Slack
- [ ] Spotify
- [ ] Tidal
- [ ] YouTube
- [ ] Zoom

## Methods of Import
The script will support parsing and grabbing relevant ranges based on the following:
1. JSON Parsing
2. Web Scraping
3. Query ARIN Assignment Database (or equal regional entity)
4. WhoIs Query

## Outputs
The script will place a file in the `lists/` directory for each service and output type. The format of each file is `[service-name]-[output-type].txt` Examples:
* `lists/amazon-web-services-ipv4.txt` - IPv4 Assignments for AWS
* `lists/amazon-web-services-ipv6.txt` - IPv6 Assignments for AWS
* `lists/amazon-web-services-url.txt` - URL List for AWS

## Configuring a Service for Import:
Add an entry to the `configs/services.yml` file with the service you desire to add: 
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
## Mapping a schema for the JSON Parser
Simple place the scheme in the `configs/schemas/` directory and add the schema to the `configs/services.yml` file.
```yaml
    services:
        - service-name: my-service
            method: "json-parse"
            schema: "my-service-schema.json"
            # Ommitted for brevity...
```