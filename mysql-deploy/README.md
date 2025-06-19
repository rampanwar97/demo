# MySQL Docker Compose Deployment Guide

This directory contains a Docker Compose configuration for deploying MySQL database.

## Prerequisites

- Docker installed on your system
- Docker Compose installed on your system
- Basic understanding of Docker and MySQL

## Project Structure

```
mysql-deploy/
├── README.md
├── docker-compose.yml
├── init.sql
└── .env.example
```

## Quick Start

1. Navigate to the mysql-deploy directory:
```bash
cd mysql-deploy
```

2. Copy `.env.example` to `.env` and update with your values:
```bash
cp .env.example .env
```

3. Update the `.env` file with your desired values:
```env
MYSQL_ROOT_PASSWORD=your_root_password
MYSQL_DATABASE=your_database_name
MYSQL_USER=your_username
MYSQL_PASSWORD=your_password
```

4. Start the MySQL container:
```bash
docker-compose up -d
```

5. Verify the container is running:
```bash
docker-compose ps
```

6. Connect to MySQL:
```bash
docker exec -it mysql_db mysql -u your_username -p
```

7. Stop the container:
```bash
docker-compose down
```

## Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| MYSQL_ROOT_PASSWORD | Root password for MySQL | - |
| MYSQL_DATABASE | Name of the database to create | - |
| MYSQL_USER | Username for the database | - |
| MYSQL_PASSWORD | Password for the user | - |

## Database Initialization

The `init.sql` file contains initial database setup with a sample users table and some test data. You can modify this file to include your own database schema and initial data.

## Persistence

The MySQL data is persisted using a Docker volume named `mysql_data`. This ensures your data survives container restarts.

## Backup and Restore

### Backup Database
```bash
docker exec mysql_db mysqldump -u root -p your_database_name > backup.sql
```

### Restore Database
```bash
docker exec -i mysql_db mysql -u root -p your_database_name < backup.sql
```

## Common Issues and Solutions

1. **Cannot connect to MySQL**
   - Check if the container is running
   - Verify the port mapping
   - Ensure credentials are correct

2. **Data persistence issues**
   - Check if the volume is properly mounted
   - Verify permissions on the host machine

## Security Considerations

1. Never commit `.env` file with real credentials
2. Use strong passwords
3. Limit port exposure if not needed externally
4. Regularly update MySQL image for security patches

## Contributing

Feel free to open issues and pull requests for improvements.

## License

MIT License