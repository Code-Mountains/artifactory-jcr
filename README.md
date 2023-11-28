### System Requirements
Before you install, please validate the system requirements provided here: https://service.jfrog.org/installer/System+Requirements  
​
### How to run
* `./config.sh` # should provide you an interactive install or upgrade
​
### Default credentials for PostgreSQL
username: artifactory
password: password

### Install or upgrade using docker volumes
* To use docker-volumes, the script `./config.sh` will not need to be run. Instead, For more deatils on install or upgrade using docker volumes refer below links and use the template `docker-compose-volumes.yaml`.

### MORE DETAILS 
For more details on installation scripts, refer: https://service.jfrog.org/installer/Installing+Artifactory

For more details on  Upgrade scripts, refer: https://service.jfrog.org/installer/Upgrading+Artifactory

For troubleshooting, refer: https://service.jfrog.org/installer/Troubleshooting

# 1st Time Install
```
$ sudo ./config.sh 


Beginning JFrog Artifactory setup


Validating System requirements

Installation Directory (Default: /root/.jfrog/artifactory): 

Running system diagnostics checks, logs can be found at [/mnt/samsung/code/artifactory/artifactory-jcr/systemDiagnostics.log]

Triggering migration script. This will migrate if needed and may take some time.

Migration logs will be available at [/mnt/samsung/code/artifactory/artifactory-jcr/bin/migration.log]. The file will be archived at [/root/.jfrog/artifactory/var/log] after installation

For IPv6 address, enclose value within square brackets as follows : [<ipv6_address>]
Please specify the IP address of this machine (Default: 127.0.0.1): 

Are you adding an additional node to an existing product cluster? [y/N]: n

The installer can install a PostgreSQL database, or you can connect to an existing compatible PostgreSQL database
(https://service.jfrog.org/installer/System+Requirements#SystemRequirements-RequirementsMatrix)
If you are upgrading from an existing installation, select N if you have externalized PostgreSQL, select Y if not.
Do you want to install PostgreSQL? [Y/n]: y

To setup PostgreSQL, please enter a password
database password: 

confirm database password: 

Creating third party directories (if necessary)

Attempting to seed PostgreSQL. This may take some time.

Successfully seeded PostgreSQL

Docker setup complete

Installation directory: [/root/.jfrog/artifactory] contains data and configurations.

Use docker-compose commands to start the application. Once the application has started, it can be accessed at [http://127.0.0.1:8082]

Examples:
cd /mnt/samsung/code/artifactory/artifactory-jcr


start postgresql:    docker-compose -p rt-postgres -f docker-compose-postgres.yaml up -d
stop  postgresql:    docker-compose -p rt-postgres -f docker-compose-postgres.yaml down
start:               docker-compose -p rt up -d
stop:                docker-compose -p rt down

NOTE: The compose file uses several environment variables from the .env file. Remember to run from within the [/mnt/samsung/code/artifactory/artifactory-jcr] folder

Done


$ docker-compose -p rt up -d
Pulling artifactory (releases-docker.jfrog.io/jfrog/artifactory-jcr:7.71.5)...
7.71.5: Pulling from jfrog/artifactory-jcr
baff9e5cc126: Already exists
1f692817f8ff: Already exists
f9695e71bfa7: Already exists
bbdfb5d90e13: Pull complete
ea9b93b2657c: Pull complete
edf72a7f5e33: Pull complete
a203a57a934a: Pull complete
477a3ac0f61c: Pull complete
5b7c38d18308: Pull complete
5898c40a264f: Pull complete
4f4fb700ef54: Pull complete
Digest: sha256:9a255759e3a6b8f8e68ff7c471c1c4ccb1c96148f82cadaba6a2d01eac178665
Status: Downloaded newer image for releases-docker.jfrog.io/jfrog/artifactory-jcr:7.71.5
Creating artifactory ... done

```

# Accept EULA License
```
curl -XPOST -vu admin:password http://localhost:8082/artifactory/ui/jcr/eula/accept

## OUTPUT:
*   Trying 127.0.0.1:8082...
* Connected to localhost (127.0.0.1) port 8082 (#0)
* Server auth using Basic with user 'admin'
> POST /artifactory/ui/jcr/eula/accept HTTP/1.1
> Host: localhost:8082
> Authorization: Basic YWRtaW46bGl2ZSRMM1RsaXZl
> User-Agent: curl/7.81.0
> Accept: */*
>
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< Content-Length: 0
< Date: Tue, 28 Nov 2023 21:43:20 GMT
< Sessionvalid: false
< X-Artifactory-Id: 0fcab7a65bf4dbd7:32949918:18c17defeca:-8000
< X-Artifactory-Node-Id: 156d5a4f55aa
< X-Jfrog-Version: Artifactory/7.71.5 77105900
<
* Connection #0 to host localhost left intact
```

# SSL Setup
```
 
sudo cp etc/nginx/sites-available/artifactory.conf /etc/nginx/sites-available/

sudo ln -s /etc/nginx/sites-available/artifactory.conf /etc/nginx/sites-enabled/artifactory.conf

sudo nginx -t

sudo systemctl reload nginx

sudo systemctl restart nginx

```