# Dockerific - Laravel, MySQL, in one Container | Docker 🐋
Run Laravel Project into Docker (Includes MySQL pre-installed)

## Instructions

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/bayuairbender2950/Dockerific
   cd Dockerific
   ```

2. **Change Database Configuration:**
   - Open the file `docker-compose.yml`.
   - Modify the following section as desired:
   ```yaml
   MYSQL_DATABASE: laravel
   MYSQL_ROOT_PASSWORD: Admin#1234
   MYSQL_PASSWORD: Admin#1234
   MYSQL_USER: laravel_user
   ```
   Make sure these settings match the configuration you'll use in step 6 to ensure a proper connection.

3. **Build Application Image:**
   ```bash
   docker compose build --no-cache
   ```
   This command builds the Docker image. The `--no-cache` option ensures the image is built from scratch, ignoring any existing cache.

4. **Run the Application:**
   ```bash
   docker compose up -d
   ```
   This command starts the Docker container in the background (`-d`).

5. **Install Composer Dependencies:**
   ```bash
   docker compose exec app composer install
   ```

6. **Copy Environment Configuration:**
   ```bash
   docker compose exec app cp .env.local .env
   ```
   Copy the sample file `.env.local` to `.env`. Be sure to change the database settings in `.env` before running the script.

7. **Run Database Migration & Seeding:**
   ```bash
   docker compose exec app ./artisan migrate:fresh --seed
   ```
   This command will:
   * Delete all existing tables in the database.
   * Recreate tables based on Laravel's migration schema.
   * Populate the database with dummy data from Laravel's seeders.

8. **Access the Web Application:**

   After successfully completing all the steps, the website can be accessed through a browser using the URL:
   **http://127.0.0.1:8000**

   The port can be changed in the `docker-compose.yml` file in the `nginx > ports` section.
