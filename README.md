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
   MYSQL_DATABASE: laravel # this optional, but better to change
   MYSQL_ROOT_PASSWORD: Admin#1234 # make sure you change this, otherwise....
   MYSQL_PASSWORD: Admin#1234 # make sure you change this, otherwise....
   MYSQL_USER: laravel_user # make sure you change this, otherwise....
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

6. **Edit & Copy Environment Configuration:**
   Edit the .env.local on Database Section
   ```env
   DB_DATABASE="laravel" # this optional, but better to change
   DB_USERNAME="laravel_user" # make sure you change this, otherwise....
   DB_PASSWORD="Admin#1234" # make sure you change this, otherwise....
   ```
   And copy the sample file `.env.local` to `.env` by running this script below. Be sure to check all configurations in `.env` before running the script.
   ```bash
   docker compose exec app cp .env.local .env
   ```
8. **Run Database Migration & Seeding:**
   ```bash
   docker compose exec app ./artisan migrate:fresh --seed
   ```
   This command will:
   * Delete all existing tables in the database.
   * Recreate tables based on Laravel's migration schema.
   * Populate the database with dummy data from Laravel's seeders.

9. **Access the Web Application:**

   After successfully completing all the steps, the website can be accessed through a browser using the URL:
   **http://127.0.0.1:8000**

   The port can be changed in the `docker-compose.yml` file in the `nginx > ports` section.
