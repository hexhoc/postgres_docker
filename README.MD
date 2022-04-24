# Introduce
**Quick start postgres container**

This dockerfile describe how to start PostgreSQL container along with a pgAdmin.
I will be using Docker (version 19.03.8), so make sure you have it installed on your machine.

# Configuration
Step by step:
1. Run docker-compose up
2. Connect to pgadmin4, for that connect to localhost:8085, enter login *user@domain.local* and password *SuperSecret*
3. Add new server. Server name is *postgres*, login *postgres* and password *postgres*
4. Have fun

# Enable logging all queries
1. Connect to postgres shell
2. Connect to database. ```psql -d postgres -U postgres```
3. Use command to locate config file ```SHOW config_file``` in this example it ```/var/lib/postgresql/data/postgresql.conf```
4. Then you need to alter these parameters inside PostgreSQL configuration file.
```
    log_statement = 'all'
    log_directory = 'log'
    log_filename = 'postgresql-%Y-%m-%d_%H%M%S.log'
    logging_collector = on
    log_min_error_statement = error
```
5. Then restart container
6. See the log. The location of the log file ```/var/lib/postgresql/data/log/```.

# Enable monitoring (pg_stat_statements)
1. Execute ```CREATE EXTENSION pg_stat_statements;```
2. Then check that extenshion is installed 
```
SELECT * 
FROM pg_available_extensions 
WHERE 
    name = 'pg_stat_statements' and 
    installed_version is not null;'
```
3. Attache shell to postgres container and then ask postgres where is conf files ```psql -U postgres -c 'SHOW config_file'```
4. Open postgresql.conf and add next 
```
# postgresql.conf
shared_preload_libraries = 'pg_stat_statements'
pg_stat_statements.max = 10000
pg_stat_statements.track = all
```
5. Restart postgres container
6. Now you can check all query ```SELECT * FROM pg_stat_statements```
