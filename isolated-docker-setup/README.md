## Isolated Docker Install Set Up

This project sets up a docker image with ES and FusionAuth at a given FusionAuth version. 

* Will run the provided kickstart file.
* Will create a directory that is based on a uniqueid passed to it.

### Prereqs

docker installed

### Usage

Run `setupspecialversion.sh` which copies the templates and update the compose files:

Some examples:

Investigate issue 253 with the latest version of FusionAuth:

```
sh setupspecialversion.sh issue253                
```

Investigate issue 253 with version 1.24 of FusionAuth:

```
sh setupspecialversion.sh issue253 1.24
```

Explore a feature in the latest version of FusionAuth:

```
sh setupspecialversion.sh tryidentitylinking
```

After the docker templates are ready to roll, `cd` to the new directory.

Modify the `kickstart/kickstart.json` file as needed to set up your instance. In particular either remove the license or add in your own license.

Then, run `docker-compose up` and you'll have a new environment for testing/using/etc.

You can only run one instance at a time (ports conflict otherwise), but you can bring them up and down as needed. Every instance will store their info separately because the compose files have unique names.

### Modifying Compose Files

If you update the docker-compose.yml and docker-compose.override.yml files, make sure you leave the `XXX` and `YYY` tokens otherwise this won't work.

### Troubleshooting

You may run out of network capacity since you'll have a lot of different networks. If you see this error message:

```
ERROR: could not find an available, non-overlapping IPv4 address pool among the defaults to assign to the network
```

run `docker network prune` to remove all unused networks. From: https://stackoverflow.com/questions/43720339/docker-error-could-not-find-an-available-non-overlapping-ipv4-address-pool-am

You can also start a container from a clean slate, if you are trying to test startup issues or kickstart. Do so by:

* running `docker volume ls` to list all volumes 
* running `docker volume rm issue253_db_dataissue253` and `docker volume rm issue253_es_dataissue253` to remove the postgresql and elasticsearch volumes
* Run `docker-compose up` to start from a clean slate.


Learn more about FusionAuth at https://fusionauth.io/

