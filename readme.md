
## Documentation: Setting up Nginx as a Global Layer for Containerized Services

### Introduction:

The goal is to establish a centralized layer using Nginx to handle requests for various containerized services. Docker Compose is utilized to manage services and networks. Custom networks play a crucial role in ensuring seamless communication between Nginx and the containerized services.

### Findings:

1. **Global Layer of Nginx:**
   - To achieve a global Nginx layer for handling requests, it is essential to have Nginx and the containerized services on the same network.

2. **Custom Network Definition:**
   - Docker Compose is used, and a custom network named `nginx_NNET` is defined.
   - The network is external, created outside of the Compose file (possibly through `docker network create`).

3. **Networking in Docker Compose:**
   - Services that need to be handled by Nginx explicitly specify the custom network.
   - Each service definition includes the `networks` attribute to assign it to the custom network.

4. **Example Configuration (Docker Compose snippet):**
   ```yaml
   version: '3'
   services:
     geospatial-api:
       build:
         context: .
         dockerfile: Dockerfile
       container_name: geospatial-api
       networks:
         - nginx_NNET
       ports:
         - "5000:5000"
   networks:
     nginx_NNET:
       external: true
   ```
   - In this example, a service named `geospatial-api` is configured to use the `nginx_NNET` network.

### Role of Custom Network:

- **Isolation and Communication:**
  - The custom network, `nginx_NNET`, acts as a bridge for communication between Nginx and containerized services.
  - It provides isolation for services while allowing them to communicate seamlessly within the same network.

### Important Note:

- **Service Network Specification:**
  - Any new service that needs to be integrated with Nginx must specify the custom network.
  - Example service configuration:
    ```yaml
    services:
      new-service:
        networks:
          - nginx_NNET
    ```
- **Example Configuration Clarification:**
  - The provided example configures the `geospatial-api` service to use the `nginx_NNET` network, ensuring it is part of the global Nginx layer.

### Conclusion:

By following the documented setup, a scalable and organized architecture is achieved. Nginx serves as a centralized point for handling requests, and the custom network ensures efficient communication between Nginx and various containerized services. The provided example and guidelines can be extended to accommodate additional services within the same architecture.

