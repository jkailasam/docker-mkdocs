#MkDocs

MkDocs is a fast, simple and downright gorgeous static site generator that's geared towards building project documentation. Documentation source files are written in Markdown, and configured with a single YAML configuration file.


##Usage
```
docker create --name=mkdocs \
-p 8000:8000 \
-e TZ="America/Los_Angeles" \
-v <path_to_mkdocs_data_folder>:/config \
-e PGID=$PGID -e PUID=$PUID \
jeeva420/mkdocs
```

##Parameters
The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side. For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container. So -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080 http://192.168.x.x:8080 would show you what's running INSIDE the container on port 80.

```
-p 8000 - the port(s)
-v /config - mkdocs Data
-e TZ for timezone information, Europe/London - see Localtime for important information
-e PGID for for GroupID - see below for explanation
-e PUID for for UserID - see below for explanation
It is based on alpine linux with s6 overlay, for shell access whilst the container is running do docker exec -it mkdocs /bin/bash.
```

##User / Group Identifiers
Sometimes when using data volumes (-v flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user PUID and group PGID. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" â¢.  
  
In this instance PUID=1001 and PGID=1001. To find yours use id user as below:
```
$ id <dockeruser>
uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```