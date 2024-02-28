
### Workflow for Adding and Enabling `main_api`:

#### Step 1: Create Configuration for `main_api`

1. Create a new configuration file for `main_api` in the `sites-available` directory.

   ```bash
   nano /etc/nginx/sites-available/main_api
   ```

   Inside the `main_api` configuration file, you would define the server block and configurations specific to `main_api`.

#### Step 2: Enable `main_api`

2. Create a symbolic link in the `sites-enabled` directory to enable `main_api`.

   ```bash
   ln -s /etc/nginx/sites-available/main_api /etc/nginx/sites-enabled/
   ```

#### Step 3: Reload Nginx

3. Reload Nginx to apply the changes.

   ```bash
   nginx -s reload
   ```

### Workflow for Adding and Enabling `ecommerce_api`:

#### Step 1: Create Configuration for `ecommerce_api`

1. Create a new configuration file for `ecommerce_api` in the `sites-available` directory.

   ```bash
   nano /etc/nginx/sites-available/ecommerce_api
   ```

   Inside the `ecommerce_api` configuration file, define the server block and configurations specific to `ecommerce_api`.

#### Step 2: Enable `ecommerce_api`

2. Create a symbolic link in the `sites-enabled` directory to enable `ecommerce_api`.

   ```bash
   ln -s /etc/nginx/sites-available/ecommerce_api /etc/nginx/sites-enabled/
   ```

#### Step 3: Reload Nginx

3. Reload Nginx to apply the changes.

   ```bash
   nginx -s reload
   ```

### Summary:

- `main_api` and `ecommerce_api` configurations are kept in the `sites-available` directory.
- Symbolic links are created in the `sites-enabled` directory to activate the configurations.
- Nginx is reloaded to apply the changes.

### Example Directory Structure:

After following these steps, you might have the following directory structure:

```plaintext
/etc/nginx/
├── sites-available/
│   ├── main_api
│   ├── ecommerce_api
│   └── ...
└── sites-enabled/
    ├── main_api -> /etc/nginx/sites-available/main_api
    ├── ecommerce_api -> /etc/nginx/sites-available/ecommerce_api
    └── ...
```

