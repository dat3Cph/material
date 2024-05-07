## Deployment Part 3 Træfik

Before you begin make sure you have the following:
- Your domain is pointing to DigitalOcean DNS servers. 
- Wildcard DNS record for your domain (*.your_domain.com)

**Remember to replace port 5173 in your Frontend Nginx configuration with port 80 and rebuild the frontend image.**

### Part 1:

Your domain has to be pointing to DigitalOcean DNS servers. This is done by adding the DigitalOcean nameservers to 
your domain provider.
[How to do](https://docs.digitalocean.com/products/networking/dns/getting-started/dns-registrars/)

### Part 2:

- Generate a digital ocean token on [DigitalOcean](https://cloud.digitalocean.com/account/api/tokens).

<img src="../images/digital_token.png">

- Copy the token and save it somewhere safe. You will need it later.

### Part 3:  Install apache2-utils inside your droplet terminal

```bash
  sudo apt-get install apache2-utils
``` 

### Part 4: Generate a traefik hashed dashboard login (droplet linux terminal )

```bash
  echo $(htpasswd -nb <your_username> <your_password>) | sed -e s/\\$/\\$\\$/g
```

<img src="../images/encrypted-password.png" alt="">

- Copy the output and save it somewhere safe. You will need it later.

### Part 5: Create a folder called acme inside the project folder

```bash
  mkdir acme
```

### Part 6: Inside the acme folder create a file called acme.json

```bash
  touch acme/acme.json
```

### Part 7: Add permissions for the acme.json file and folder

```bash
  chmod 600 ./acme
  chmod 600 ./acme/acme.json
```

### Part 8: Create a .env file inside the project folder and add the following environment variables

```bash
# Lets-encrypt - Digital Ocean
PROVIDER=digitalocean
EMAIL=<your_email>
ACME_STORAGE=/etc/traefik/acme/acme.json
DO_AUTH_TOKEN=<your_digital_ocean_token> (see step 2)

# Traefik
TRAFIK_DOMAIN=traefik.<your_domain>
DASHBOARD_AUTH=<your_traefik_dashboard_login> (see step 3 and 4)

# Rest API
API_DOMAIN=api.<your_domain_name>

# Frontend
FRONTEND_DOMAIN=<your_domain_name>

# Postgres User
POSTGRES_USER=<your_postgres_user>
POSTGRES_PASSWORD=<your_postgres_password>

# Watchtower
REPO_USER=<your_docker_hub_username>
REPO_PASS=<your_docker_hub_password>

# REST API SETUP
CONNECTION_STR=jdbc:postgresql://db:5432/
DB_USERNAME=<your_postgres_user_2> # (has to be different from the first one. See Part 10)
DB_PASSWORD=<your_postgres_password_2> # (has to be different from the first one. See Part 10)
DEPLOYED=TRUE
SECRET_KEY=super_secret_key (has to include at least 32 characters letters and numbers)
TOKEN_EXPIRE_TIME=1800000 (30 minutes)
ISSUER=<your_domain> or something like "3sem.dk"

```

### Part 9: Create a docker-compose.yml file inside the project folder and add the following code from the link below

- [docker-compose gist](https://gist.github.com/tysker/0faa2bd46cddbda32f26d4f944120516)


### Part 10: Create a sql file

- Create a folder called db inside the project folder and add a file called init.sql
- Add the following code to the init.sql file
- Replace the placeholders with your own values.
- The placeholders are:
  - <CHANGE_USER>
  - <CHANGE_PASSWORD>
  - <CHANGE_DATABASE_NAME>

```sql
CREATE ROLE '<CHANGE_USER>' PASSWORD '<CHANGE_PASSWORD>' LOGIN CREATEDB;
GRANT pg_read_all_data TO <CHANGE_USER>;
GRANT pg_write_all_data TO <CHANGE_USER>;
SET ROLE dev;

-- create databases
CREATE DATABASE company;
CREATE DATABASE <CHANGE_DATABASE_NAME>;

\connect <CHANGE_DATABASE_NAME>;
GRANT ALL PRIVILEGES ON DATABASE <CHANGE_DATABASE_NAME> TO <CHANGE_USER>;

\connect company;
GRANT ALL PRIVILEGES ON DATABASE company TO <CHANGE_USER>;

CREATE TABLE companies
(
    company_id   SERIAL PRIMARY KEY,
    company_name VARCHAR(255) NOT NULL
);

CREATE TABLE contacts
(
    contact_id   SERIAL PRIMARY KEY,
    company_id   INT,
    contact_name VARCHAR(255) NOT NULL,
    phone        VARCHAR(25),
    email        VARCHAR(100),
    CONSTRAINT fk_company
        FOREIGN KEY (company_id)
            REFERENCES companies (company_id)
);

-- insert data
INSERT INTO companies(company_name)
VALUES ('BlueBird Inc'),
       ('Dolphin LLC');

INSERT INTO contacts(company_id, contact_name, phone, email)
VALUES (1, 'John Doe', '(408)-111-1234', 'john.doe@bluebird.dev'),
       (1, 'Jane Doe', '(408)-111-1235', 'jane.doe@bluebird.dev'),
       (2, 'David Wright', '(408)-222-1234', 'david.wright@dolphin.dev');
```

### Part 11:

- Run `docker-compose up -d` inside the project folder to start the services.

<img src="../images/3sem-setup-remote.drawio.png" alt="3 semester local environment setup">
