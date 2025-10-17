# 🔄 Upgrading Self-Hosted Twenty CRM

This guide walks you through the process of upgrading a self-hosted Twenty CRM instance. It assumes you have a working Docker Compose installation of Twenty CRM.

## 📋 Prerequisites

- A working Twenty CRM installation using Docker Compose
- SSH access to your server
- Basic command line knowledge
- Docker and Docker Compose installed
- Server with sufficient disk space for database backups

## ⚠️ Important Notes

- **Always make a database backup before upgrading**
- Twenty CRM needs to be upgraded sequentially through available versions (e.g., v0.44 → v0.50 → v0.51 → v0.52)
- You cannot skip major versions during the upgrade process
- Check GitHub releases to identify the correct upgrade path (sometimes version numbers may skip)
- The upgrade process involves downtime
- Ensure you have enough disk space for database backups

## 🛠️ Step 1: Identify Your Containers

First, identify your container names for reference:

```bash
# List all running containers with their names and images
docker ps --format "table {{.Names}}\t{{.Image}}\t{{.Status}}"

# List all containers (including stopped ones)
docker ps -a --format "table {{.Names}}\t{{.Image}}\t{{.Status}}"
```

!!! tip "Tip: Take note of"
    - Your database container name (usually `twenty-db-1` or similar)
    - Your server/application container name (usually `twenty-server-1` or similar)

## 💾 Step 2: Create a Database Backup

Before starting any upgrade process, create a full backup of your database:

```bash
# Create a dated backup file
docker exec -it <db_container_name> pg_dumpall -U postgres > twenty_backup_$(date +%Y%m%d).sql
```

Verify that the backup file exists and is not empty:

```bash
ls -lh twenty_backup_*.sql
```

## 🔄 Step 3: Sequential Upgrade Process

Follow these steps for each version upgrade (e.g., upgrading from v0.X.Y to v0.X+1.Z):

1. Stop your current Twenty CRM:

    ```bash
    cd /path/to/your/twenty/installation
    docker compose down
    ```

2. Update the TAG in your `.env` file:

    ```bash
    # Edit your .env file
    nano .env

    # Find the TAG line and change it to the next sequential version:
    TAG=0.X+1.Z
    ```

3. Start Twenty CRM with the new version:

    ```bash
    docker compose up -d
    ```

4. Run the migration commands:

    ```bash
    # Replace <server_container_name> with your actual server container name
    docker exec -it <server_container_name> yarn database:migrate:prod
    docker exec -it <server_container_name> yarn command:prod upgrade
    ```

5. Verify that the upgrade was successful:

    ```bash
    docker ps
    # Check logs if needed
    docker logs <server_container_name>
    ```

6. Create another backup before proceeding to the next version:

    ```bash
    docker exec -it <db_container_name> pg_dumpall -U postgres > twenty_backup_v<version>_$(date +%Y%m%d).sql
    ```

7. Repeat steps 1-6 for each sequential version upgrade

## 🔄 Version-Specific Commands

Some versions may require specific upgrade commands. Always check the [official upgrade guide](https://twenty.com/developers/section/self-hosting/upgrade-guide) for version-specific instructions.

Examples of version-specific commands:

```bash
# For version 0.33 upgrade
docker exec -it <server_container_name> yarn command:prod upgrade-0.33

# For version 0.34 upgrade
docker exec -it <server_container_name> yarn command:prod upgrade-0.34

# For other versions, the command may simply be:
docker exec -it <server_container_name> yarn command:prod upgrade
```

## 🔄 Upgrading to Patch Versions

For patch version upgrades within the same major/minor version (e.g., v0.52.0 to v0.52.9):

1. Create a backup:

    ```bash
    docker exec -it <db_container_name> pg_dumpall -U postgres > twenty_backup_$(date +%Y%m%d).sql
    ```

2. Update the TAG in your `.env` file:

    ```bash
    # Edit your .env file
    nano .env

    # Find the TAG line and change it to the latest patch version:
    TAG=0.X.Y+1
    ```

3. Restart:

    ```bash
    docker compose down
    docker compose up -d
    ```

For patch versions within the same major/minor version, running migration commands is typically not necessary, but always check the release notes to be sure.

## ✅ Post-Upgrade Verification

After completing each upgrade step:

1. Verify all containers are running:

    ```bash
    docker ps
    ```

2. Check the application logs for any errors:

    ```bash
    docker logs <server_container_name>
    ```

3. Access your Twenty CRM through the browser to ensure it's working correctly

4. Verify that your existing data is intact

## 🔧 Troubleshooting

If you encounter issues during the upgrade:

- **Database migration failures**: Restore from your backup and check the logs
- **Container won't start**: Check logs with `docker logs <server_container_name>`
- **Missing data after upgrade**: Restore from backup and try again
- **Wrong container for migration commands**: Ensure you're running commands on the server container, not the database container
- **Version mismatch errors**: You may need to run a version-specific upgrade command (e.g., `yarn command:prod upgrade-0.X`)

To restore from a backup if needed:

```bash
cat your_backup_file.sql | docker exec -i <db_container_name> psql -U postgres
```

## 📚 Additional Resources

- [Official Twenty CRM Upgrade Guide](https://twenty.com/developers/section/self-hosting/upgrade-guide)
- [Twenty CRM GitHub Repository](https://github.com/twentyhq/twenty)
- [Docker Compose Documentation](https://docs.docker.com/compose/)

---

*Last updated: May 8, 2025 - Author: Wesley Ordonez*
