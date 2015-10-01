# Purpose

Create quick time to value on the installation and upkeep of the Prometheus
and cAdvisor monitoring solution.

# Usage

You will need to replace the environment variables for the `dynamic-haproxy` 
service.  

* SE_LEADER_IP: This is the private (routable) IP address or FQDN of your 
  StackEngine mesh leader. It is used to keep up with the hosts in the mesh and
  cAdvisor.
* SE_API_TOKEN:  This is your Container Application Center (CAC) API Token. 
  It is used by `confd` to connect to the CAC Service Discovery layer.
* SE_CADVISOR_KEY: The service discovery key to check for changes. (See below
  for how to construct them.)
* SE_CADVISOR_RANGE: In most cases this will be nearly identical to the KEY. 
  (See below for how to construct them.)

## Constructing a Service Discovery Key and Range

The construction of a Service Discovery key is done as follows:

* "apps/" + {{instance_name}} + "-" + {{service_name}} + "-" + {{exposed_ port}} + "/containers"

The `instance` is what you set when clicking the "Launch" 
button after saving the YAML file in the Advanced Editor.

The `service_name` is defined when dragging a component into the editor 
graphically as the "Name".  It is also seen as the service name in the YAML.

The `exposed_port` is the _internally_ exposed port for the backend container. 
For cAdvisor, this will typically be 8080.   

In the case of `prometheus-cadvisor.yml`, that would be the line reading 
"cadvisor:".

Given that you name the instance prom-cadv and the cAdvisor service
"my-cadvisor", and that cAdvisor is listening on port 8080 inside the container 
the key would be

`apps/cadv-prom-my-cadvisor-8080/containers` 

and the range would be:

`/apps/cadv-prom-my-cadvisor-8080/containers/*`

# License

MIT