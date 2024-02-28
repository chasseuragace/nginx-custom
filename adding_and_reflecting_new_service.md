
### Tutorial: Adding a New Service (`main_api`) to Nginx Network

#### Step 1: Create Nginx Configuration File for `main_api`

1. In your `nginx-conf` folder, create a new configuration file specific to the `main_api`. For example, `main_api.conf`.

   ```nginx
   # nginx-conf/main_api.conf

   server {
       listen 80;
       server_name main_api;

       location /main/ {
           proxy_pass http://main_api:5000/;
           proxy_set_header Host $host;
           proxy_set_header X-Real-IP $remote_addr;
           proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
           proxy_set_header X-Forwarded-Proto $scheme;
       }

       # Additional settings if needed...
   }
   ```

   In this example, the `proxy_pass` directive forwards requests to the `main_api` service on port `5000`. Adjust the configuration based on your specific needs.

#### Step 2: Verifying Docker Compose File for the new sercice

2. In your Docker Compose file, make sure to include the new service (`main_api`) and ensure it's connected to the `nginx_NNET` network.

   ```yaml
   version: '3'
   services:
     main_api:
       # Configuration for main_api service
       networks:
         - nginx_NNET
       # other configuration...
   networks:
     nginx_NNET:
       external: true
   ```

#### Step 3: Run Docker Compose

3. Run Docker Compose to bring up the Nginx and `main_api` services.

   ```bash
   docker-compose up -d
   ```

#### Step 4: Access `main_api` through Nginx

4. Access the `main_api` service through Nginx using the path `/main/...`. For example, if your `main_api` exposes an endpoint at `/api/resource`, you can access it through Nginx at `http://nginx/main/api/resource`.

### Explanation:

- **Nginx Configuration File (`main_api.conf`):**
  - The `location /main/` block in the Nginx configuration file is responsible for proxying requests to the `main_api` service.
  - `proxy_pass` is set to the address of the `main_api` service, and other headers are configured to pass along relevant information.

- **Docker Compose File:**
  - The `main_api` service is added to the Docker Compose file, and it is connected to the `nginx_NNET` network to enable communication with Nginx.

- **Run Docker Compose:**
  - The Docker Compose command is used to bring up the Nginx and `main_api` services.

- **Access through Nginx:**
  - Access the `main_api` service through Nginx using the specified path (`/main/...`).

By following these steps, you can easily add a new service to the Nginx network and configure a reverse proxy to access it through a specific path. This approach allows for a modular and maintainable Nginx configuration without directly modifying the Docker image.

##Reloading Nginx With updated configuration
 you need to reload the Nginx configuration to reflect the changes made in the `nginx-conf` folder, follow these steps:

1. Find the name of the Nginx container using the `docker ps` command:

   ```bash
   docker ps
   ```

   Look for the container running the Nginx service. In your case, it appears to be named something like `nginx-nginx-1` depending upon you folder configuration. Take note of the container name or ID.

2. Reload the Nginx configuration using the `docker exec` command:

   ```bash
   docker exec nginx-nginx-1 nginx -s reload
   ```

   Replace `nginx-nginx-1` with the actual name or ID of your Nginx container.

This command sends the `reload` signal to the Nginx process inside the container, causing it to reload the configuration without restarting the entire container. This allows the changes made in the `nginx-conf` folder to take effect.

Please ensure that the Nginx container is currently running when you execute the reload command. If the container is not running, start it first using `docker-compose up -d` or a similar command.