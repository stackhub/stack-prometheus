# Purpose

Create quick time to value on the installation and upkeep of the Prometheus
and cAdvisor monitoring solution.

# Usage

You will need to replace the environment variables for the `dynamic-haproxy` 
service.  

* SE_API_TOKEN:  This is your Container Application Center (CAC) API Token. 
  It is used by `confd` to connect to the CAC Service Discovery layer.
* SE_LEADER_IP: The private IP address of the mesh leader.  
* SE_SERVICE_DISCOVERY_KEY: The portion of the service discovery 
  key to check for changes. cAdvisor containers write their address
  and port to this serivce key. (See below for how to construct them.)


## Constructing a Service Discovery Key and Range

The construction of a Service Discovery key is done as follows:

* {{application_instance_name}} + "-" + {{service_name}} + "-" 
  + {{exposed_ port}} 

The `application_instance_name` is what you set when clicking the
"Launch" button.

The `service_name` is defined when dragging a component into the editor 
graphically as the "Name".  It is also seen as the service name in the YAML.

The `exposed_port` is the _internally_ exposed port for the backend container. 
For cAdvisor, this will typically be 8080.   

In the case of `prometheus-cadvisor.yml`, that would be the line reading 
"cadvisor:".

Given that you name the instance prom-cadv and the cAdvisor service
"my-cadvisor", and that cAdvisor is listening on port 8080 inside the container 
the key would be

`cadv-prom-my-cadvisor-8080` 

# License

MIT