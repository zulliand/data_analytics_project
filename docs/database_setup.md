# PostgreSQL Database Setup Guide

## Overview
This guide explains how to set up and use the PostgreSQL database integration for the Weather & Bicycle Usage project.

## Prerequisites
- Docker installed and running
- Python 3.x with pip
- psycopg2-binary package

## Quick Start

### 1. Start PostgreSQL Container
```bash
cd /workspaces/data_analytics_project
docker compose up -d
```

This command will:
- Pull the PostgreSQL 15 image (if not already present)
- Create a persistent volume for data storage
- Start the container in detached mode
- Expose port 5432 on localhost

### 2. Verify Container Status
```bash
docker ps | grep postgres
```

You should see `postgres_container` running.

### 3. Install Python Dependencies
```bash
pip install psycopg2-binary
```

### 4. Run Database Notebook
Open and execute `notebooks/05_database.ipynb` sequentially.

## Database Configuration

### Connection Parameters
- **Host**: localhost
- **Port**: 5432
- **Database**: weatherbike
- **User**: student
- **Password**: student123

### Database Schema

#### Table: bikes_weather
```sql
CREATE TABLE bikes_weather (
    time TIMESTAMP PRIMARY KEY,
    temperature FLOAT,
    humidity FLOAT,
    windspeed FLOAT,
    precipitation FLOAT,
    bike_count INT
);
```

## Features Demonstrated

### 1. Database Connection
- Establish connection using psycopg2
- Verify connection with version query
- Proper error handling

### 2. Table Management
- CREATE TABLE IF NOT EXISTS
- Primary key constraint
- Data type selection

### 3. Data Insertion
- Bulk insert with ON CONFLICT handling
- Transaction management (commit/rollback)
- Progress tracking

### 4. SQL Queries
- SELECT with LIMIT
- WHERE clause filtering
- ORDER BY sorting
- Aggregate functions (AVG, MAX, MIN)
- ROUND for numeric formatting

### 5. Data Integration
- Loading data from CSV
- Type conversion (datetime, int)
- Pandas integration with read_sql()

### 6. Visualization
- Query data from PostgreSQL
- Create matplotlib visualizations
- Display database-driven insights

## Useful Commands

### Stop the Container
```bash
docker compose down
```

### Stop and Remove Data
```bash
docker compose down -v
```

### View Container Logs
```bash
docker logs postgres_container
```

### Access PostgreSQL Shell
```bash
docker exec -it postgres_container psql -U student -d weatherbike
```

### Check Database Size
```sql
SELECT pg_size_pretty(pg_database_size('weatherbike'));
```

### List All Tables
```sql
\dt
```

### Describe Table Structure
```sql
\d bikes_weather
```

## Troubleshooting

### Port Already in Use
If port 5432 is already taken:
1. Stop other PostgreSQL instances
2. Or modify `docker-compose.yml` to use a different port:
   ```yaml
   ports:
     - "5433:5432"
   ```
   Then update connection host in notebook to `localhost:5433`

### Connection Refused
- Ensure Docker is running
- Wait 5-10 seconds after starting container
- Check container status: `docker ps`

### Permission Denied
- Ensure Docker daemon is running with proper permissions
- On Linux, you may need to add your user to the docker group:
  ```bash
  sudo usermod -aG docker $USER
  ```

### Data Not Persisting
- Check volume exists: `docker volume ls`
- Ensure you're not using `-v` flag when stopping: `docker compose down` (not `docker compose down -v`)

## Performance Tips

### Batch Inserts
For better performance with large datasets, use batch inserts:
```python
cursor.executemany(insert_query, data_batch)
```

### Create Indexes
For faster queries on non-primary-key columns:
```sql
CREATE INDEX idx_temperature ON bikes_weather(temperature);
CREATE INDEX idx_bike_count ON bikes_weather(bike_count);
```

### Use COPY for Bulk Loading
For very large datasets:
```python
from io import StringIO
cursor.copy_from(StringIO(csv_data), 'bikes_weather', sep=',')
```

## Security Notes

**⚠️ WARNING**: The current setup uses simple credentials for educational purposes only.

For production environments:
- Use strong passwords
- Store credentials in environment variables
- Use SSL/TLS connections
- Implement proper user access controls
- Regular backups

## Bonus Points Justification

This PostgreSQL integration demonstrates:
1. **Professional Data Management**: Beyond CSV files
2. **Docker Proficiency**: Container orchestration
3. **SQL Skills**: Multiple query types and optimization
4. **Integration**: Seamless Python-Database workflow
5. **Best Practices**: Error handling, transactions, connection management

## Additional Resources

- [PostgreSQL Documentation](https://www.postgresql.org/docs/15/)
- [psycopg2 Documentation](https://www.psycopg.org/docs/)
- [Docker Compose Reference](https://docs.docker.com/compose/)
- [SQL Tutorial](https://www.postgresql.org/docs/15/tutorial.html)

---

**Author**: ZHAW Data Analytics Project  
**Date**: December 2025  
**Version**: 1.0
