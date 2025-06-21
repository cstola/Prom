Setting up **Prometheus and Grafana**  on local **_Docker Desktop for Windows_** 

1. If the entire solution exists in seperate containers within the **compose stack** built by _docker compose up -d_ based on _docker-compose.yaml_ file, there is no need for specifying network parameter as it will be created by default and used internaly by all services within the stack

2. To check in the browser whether a single service is running properly there is a need to expose it through the **ports mapping** within the service definition block, like: 
> ports: <br>- '9090:9090'

3. When connecting Grafana to Prometheus which is exposed on the host at `localhost:9090`, avoid using `127.0.0.1:9090` in the Grafan UI from within a container - this IP refers to the Grafana container itself, not the host. Two reliable options are:
- `http://host.docker.internal:9090` - connects to Prometheus running on the hos
- `http://prometheus:9090` - connects to Prometheus via its service name within the internal Docker network, as defined in _docker-compose.yaml_
