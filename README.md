# Description
PyNetSecWatch is a simple Python tool that will allow you to parse webpages, WhoIs, ARIN, and other sources to generate complete lists of all known address and ports for a configured service. This is a smaller component of a project I'm working on that will parse for common services and create a REST API and Webpage users can use for a centralized list of all known service information and firewall rules that would be needed to allow, deny, or log traffic to a specific service. This is just a project to help me along my DevNet studies, obviously things like this already exist, but what fun is using something that exists when you can create your own?
create 


## Outputs
The script will place a file in the `lists/` directory for each service and output type. The format of each file is `[service-name]-[output-type].txt` Examples:
* `lists/amazon-web-services-ipv4.txt` - IPv4 Assignments for AWS
* `lists/amazon-web-services-ipv6.txt` - IPv6 Assignments for AWS
* `lists/amazon-web-services-url.txt` - URL List for AWS

## Documentation Table of Contents
* [Services - About and Configuration](docs/Services.md) - docs/Services.md