                                     |
Docker provides several network drivers, but a few are especially important in day-to-day use:

| Network Type | Description                                                                                                                    | Common Use Case                                                                                       |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------- |
| **Bridge**   | Default network driver for containers on a single host. Containers can communicate with each other through the bridge network. | Web app + database running on the same Docker host.                                                   |
| **Host**     | Container shares the host machine's network stack. No network isolation between host and container.                            | High-performance networking, monitoring tools, or applications that need direct access to host ports. |
| **None**     | Disables networking for the container.                                                                                         | Security-sensitive workloads or containers that don't require network access.                         |
| **Overlay**  | Connects containers across multiple Docker hosts. Used with Docker Swarm.                                                      | Distributed microservices running on several servers.                                                 |
| **Macvlan**  | Assigns a unique MAC address and IP address to each container, making it appear as a physical device on the network.           | Legacy applications that require direct network visibility.                                           |
| **IPvlan**   | Similar to Macvlan but shares the parent interface's MAC address while assigning separate IPs.                                 | Large-scale deployments where MAC address limits are a concern.                                       |

### Most Commonly Used Types

#### 1. Bridge Network

```bash
docker network create my-bridge
docker run -d --network my-bridge nginx
```

Features:

* Default for standalone containers.
* Internal DNS resolution by container name.
* Network isolation from the host.

#### 2. Host Network

```bash
docker run --network host nginx
```

Features:

* No NAT.
* Better network performance.
* Port mappings (`-p`) are ignored.

#### 3. Overlay Network

```bash
docker network create -d overlay my-overlay
```

Features:

* Multi-host communication.
* Service discovery.
* Common in Docker Swarm clusters.

#### 4. Macvlan Network

```bash
docker network create -d macvlan \
  --subnet=192.168.1.0/24 \
  --gateway=192.168.1.1 \
  -o parent=eth0 my-macvlan
```

Features:

* Container gets its own LAN IP.
* Useful when containers must be reachable directly from the physical network.

### Quick Interview Summary

* **Bridge** → Containers communicate on the same host (default).
* **Host** → Container uses host networking directly.
* **None** → No networking.
* **Overlay** → Containers communicate across multiple hosts.
* **Macvlan/IPvlan** → Containers appear as separate devices on the physical network.

You can view available networks with:

```bash
docker network ls
```

And inspect a network with:

```bash
docker network inspect <network-name>
```

