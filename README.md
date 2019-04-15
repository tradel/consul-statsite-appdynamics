# consul-statsite-appdynamics

Simple instructions:

 1. Download the AppDynamics [machine agent], unzip, and configure it for [standalone mode].
 2. Go to the `monitors` folder and clone this repo into a subfolder named `StatSite`.
 
        git clone https://github.com/tradel/consul-statsite-appdynamics.git StatSite

 3. Download (or compile) a [statsite binary] and place it in the `monitors/StatSite` folder.

 3. Start the machine agent. You will probably need to increase the value of `maxMetrics` so that data doesn't get truncated.
 
        java -Xmx64m -Dappdynamics.agent.maxMetrics=10000 -jar machineagent.jar
 
 3. Configure consul with a [telemetry stanza] to send metrics to statsite.

        {
            "telemetry": {
                "statsite_address": "localhost:8125"
            }
        }

 4. Restart Consul. 


[machine agent]: https://download.appdynamics.com/download/#version=&apm=machine&os=&platform_admin_os=&appdynamics_cluster_os=&events=&eum=&page=1
[standalone mode]: https://docs.appdynamics.com/display/PRO45/Configure+the+Standalone+Machine+Agent
[telemetry stanza]: https://www.consul.io/docs/agent/options.html#telemetry
[statsite binary]: https://github.com/statsite/statsite/blob/master/INSTALL.md
