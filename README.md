# Using Fallow in a Ubuntu WSL Docker Container
We have taken a completly different approach to running Fallow in a Docker Container in Ubuntu server

## The assumption is:
That you have installed Ubuntu, either as a server or in Windows 11 using WSL 

And that you have the software you want to analyze cloned from git in this folder: \
C:\UnSynchronized\ProjectsAZDO 

However if you have it in a different folder then change this in the compose.yaml file: \
mnt/c/UnSynchronized/ProjectsAZDO \
Here:
```sh
    volumes:
      - /mnt/c/UnSynchronized/ProjectsAZDO:/opt/ProjectsAZDO
```

## Setup the Compose file 
```sh
# Create the fallow folder in your Docker Stacks
mkdir -p /opt/stacks/fallow

cd /opt/stacks/fallow

# Pull down the Docker components
docker compose pull

# Always start this container in Detached mode
docker compose up -d

# Now you are ready to use Fallow running in the Docker container
```

**To start Fallow in the Ubuntu server**
```sh
cd /opt/stacks/fallow

./start.sh
```
**To run reports in the Docker Container**
```sh
# Open project folder
cd /opt/ProjectsAZDO/<project folder>

#Run Dead Code Analysis
fallow dead-code --format markdown --output-file dead-code.md

# Run Hotspot Analysis
fallow health --format markdown --score --output-file health.md

# Run Duplicate Code Analysis
fallow dupes --format markdown --output-file dupes.md

# To produce an Analysis Summary 
fallow --format markdown --summary --output-file summary.md
```

**To view reports**
```sh
# List latest reports (on top )
ls -lt /mnt/c/UnSynchronized/ProjectsAZDO/<project folder>
```
