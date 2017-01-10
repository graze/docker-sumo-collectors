# Sumologic Collector Templates

![Giphy](https://media3.giphy.com/media/39jFTKBiaeo1O/giphy.gif)

A set of sumologic collectors using templates

## Why?

The default set of sumologic collectors put all the logs within a single category or use a generated name so un-referencable (boo). This provides a set of templates that uses the environment variable: `LOG_APPLICATION` in the collector name and category

Environment Variables:

- `LOG_APPLICATION` - name of the application to appear in the name / category
- `ENVIRONMENT` - the environment of the logs (live,stage,dev,etc)

## Collectors

### Apache

image: `graze/sumo-collectors:apache`

The apache collector looks at: `/var/log/apache2/*_access.log` files and uses the category: `apache/${LOG_APPLICATION}/${ENVIRONMENT}`
It also looks at: `/var/log/apache2/error.log` and reports it as: `app/${LOG_APPLICATION}/${ENVIRONMENT}`

### Docker

image: `graze/sumo-collectors:docker`

The docker collector connects to the docker sock on the host machine and reports logs and stats to sumologic.

- logs -> category: `docker/logs/${LOG_APPLICATION}/${ENVIRONMENT}`
- stats -> category: `docker/stats/${LOG_APPLICATION}/${ENVIRONMENT}`

#### Docker logs

image: `graze/sumo-collectors:docker-logs`

A logs only collector for docker (does not send that stats stream to reduce the amount of log messages being sent)

- logs -> category: `docker/logs/${LOG_APPLICATION}/${ENVIRONMENT}`

### File

image: `graze/sumo-collectors:file`

The file collector recursively looks at a directory and sends all the log files with category: `logs/${LOG_APPLICATION}/${ENVIRONMENT}`
