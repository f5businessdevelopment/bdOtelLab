Exercise 2 - Exporting NGINX Plus spans and metrics using Open Telemetry 
============================================================================

During this exercise, you will be 



#### Review NGINX configuration file

From the VS Code UI use the navigation pane on the left and open the NGINX Plus configuration file, (*nginx.conf*).  Familiarize yourself with the configuration file contents.  

#### Review OTel Collector configuration

The OpenTelemetry Collector service provides a vendor-agnostic proxy to receive, process and export observability data.  The collector supports open-source observability data formats (e.g. Jaeger, Prometheus, Fluent Bit, etc.) sending to one or more open-source or commercial back-ends.

The OTel collector is managed via a user-readable YAML configuration file.  At a minimum, the configuration must include the following three sections:
- **Receivers** - section with information related to how the collector will receive observability data, (i.e. protocols, endpoint addresses, ports) 

- **Processors** - section with configuration information related to data manipulation and insertion.  In this section, one can add/delete/modify data streams using filters.

- **Exporters** - section including information related push or pull based backends/destinations

From the VS Code UI use the navigation pane on the left and open the OTel collector gateway configuration file, (*collector-gateway.yml*).  Familiarize yourself with the configuration file contents.  Specific to this exercise, the collector configuration file, (*example below*)  has been configured to:
 - Receive telemetry from a published NGINX status page
 - Process records using the standard batch processor
 - Export metrics to a Prometheus backend

<img src= "../images/Picture18.png">





**Go to [Exercise 3 - Exporting BIG-IP metrics using the OTel consumer](ex3.md)**

**Go to [Overview](overview.md)**

**Go [Home](https://github.com/f5businessdevelopment/bdOtelLab)**
