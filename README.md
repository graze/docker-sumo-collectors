# Sumologic Collector Templates

A set of sumologic collectors using templates

## Why?

The default set of sumologic collectors put all the logs within a single category or use a generated name so un-referencable (boo). This provides a set of templates that uses the environment variable: `LOG_APPLICATION` in the collector name and category

## Collectors

### Apache

The apache collector looks at: `/var/log/apache2/*_access.log` files and uses the category: `${LOG_APPLICATION}/apache` It also looks at: `/var/log/apache2/error.log` and reports it as: `${LOG_APPLICATION}/app`

### Docker

The docker collector connects to the docker sock on the host machine and reports logs and stats to sumologic.

- logs -> category: `${LOG_APPLICATION}/docker/logs`
- stats -> category: `${LOG_APPLICATION}/docker/stats`

### File

The file collector recursively looks at a directory and sends all the log files with category: `${LOG_APPLICATION}/file`
