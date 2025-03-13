Exercise 2 - Exporting NGINX Plus spans and metrics using Open Telemetry 
============================================================================

With our application now functioning correctly and delivering trace data to Jaeger, we'll now expand our observability to include our front-end load balancer, (NGINX Plus).  

### Configure NGINX tracing - review and update the NGINX configuration file

The lab environment includes an NGINX Plus instance that has been configured to publish and provide load balancing to our previously deployed application, (thelabApp).  The application can be reached at *http://10.1.10.4*.  

NGINX uses a configuration file (nginx.conf) to define its behavior, including server blocks, reverse proxy settings, load balancing, security rules, logging, and performance optimizations.  During this exercise, you will modify the *nginx.conf* file to enable the sending of trace information, (*spans*) to Jaeger. 

From the VS Code UI use the navigation pane on the left and open the NGINX Plus configuration file, (*nginx.conf*).  Familiarize yourself with the configuration file contents, (see below).  

<img src= "../images/Picture39.png">

Several lines related to OTel integration have been "remmed out".  Let's review the lines and remove the leading '#' to enable to line item.

- Line 2 - The [NGINX Open Telemetry module](https://docs.nginx.com/nginx/admin-guide/dynamic-modules/opentelemetry/) has been installed on the lab NGINX instance.  The module provides OTel distributed tracing support and must also be loaded via the NGINX configuration.  Remove the leading '#' to enable loading of the module.

   <img src= "../images/Picture40.png">

- Line 10 - The '*otel_service_name*' directive sets the trace stream's service name.  All spans generated will be categorized and grouped under this service name, (see below). Remove the leading '#' to set the service name.

    <img src= "../images/Picture41.png">

- Lines 11 thru 13 - The '*otel_exporter*' directive block is used to specify the address of the destination service. For this lab, we have specified the locally hosted Jaeger endpoint. Remove the leading '#' to set the export destination.

   <img src= "../images/Picture42.png">
- Line 22 - The '*otel_trace*' directive flag determines whether tracing is enabled. Remove the leading '#' to enable tracing.  

   <img src= "../images/Picture43.png">

- Line 25 - The '*otel_span_name*' directive sets the event span name. Remove the leading '#' to set the span name.
- Line 26 - In additionn to the default attributes provided, the '*otel_span_attr*' directive can be used to assign custom attributes, (key/value). Remove the leading '#' to create a custom span attribute. 
- Line 27 - The '*otel_trace_context*' directive determines how the trace context relates to other traces. Remove the leading '#' to set trace context.

   <img src= "../images/Picture44.png">

With the above noted file lines updated, save the file and use the following command to verify and reload the NGINX configuration:

```sudo nginx -t && sudo nginx -s reload```

#### Verify NGINX tracing
Once you have reloaded NGINX refresh the application (http://10.1.10.4) a few times then return to the Jaeger UI, refresh the page.  From the Jaeger UI select the '*NGINX*' service and search for the latest traces by selecting *'**Find Traces**'*, (see below).

<img src= "../images/Picture45.png">

Review the various spans paying special attention to the NGINX span '*LB Frontend call*' tags.  In addition to the default tags provided, you should be able to find the custom span attribute configured via the NGINX configuration file.

### Configure NGINX metrics - review OTel Collector configuration and update the NGINX configuration file

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
