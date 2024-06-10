Exercise 3 - Exporting BIG-IP Next logs using Open Telemetry
============================================================================

During this exercise, you will be using BIG-IP Next Central Manager to configure a BIG-IP Next instance to send logs to a locally installed Splunk Enterprise instance by way of the OpenTelemetry collector.

The OpenTelemetry Collector has been configured, as noted earlier, with a Splunk logs exporter, (see below).  

<img src="../images/Picture26.png" width=300>

You will use BIG-IP Next Central Manager to configure remote logging for one of the managed BIG-IP Next Instances.  

<img src="../images/Picture27.png">

<img src="../images/Picture28.png">

Take a few minutes to explore the UI.  This BIG-IP Next environment includes, in addition to the Central Manager, a single BIG-IP Next instance hosting a single application deployment, theLabApp.  

If your example application is still running, you should see the application with a *Good* health, (see below).

<img src="../images/Picture29.png">

*awk 'NF {sub(/\r/, ""); printf "%s\\n",$0;}' cert-name.pem*

<img src="../images/Picture30.png">

**Go to [Overview](overview.md)**

**Go [Home](https://github.com/f5businessdevelopment/bdOtelLab)**