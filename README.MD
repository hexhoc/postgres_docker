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