# Notes to be organised & assorted



############################################################################


### Repos and Pushing
With a free account, Dockerhub allows you to make unlimited Public repos, and ONE private.

- Create public repo, named 101-todo-app

Applying a tag within terminal:

- Login using `docker login -u [username]`
- Apply tag using `docker tag docker-101 YOUR-USER-NAME/[tag-name]`
- Push container into repo using `docker push YOUR-USER-NAME/101-todo-app`

### Using Ubuntu (or other OS)
Containers can contain OS systems such as Linux Ubuntu. The following line of code creates an Ubuntu container, with a file `/data.txt`, containing a random number between 1 and 10,000:

`docker run -d ubuntu bash -c "shuf -i 1-10000 -n 1 -o /data.txt && tail -f /dev/null"`


#### Persistance
Containers have so far effectively been 'Read Only'. Changes isolated to a removed container will be lost.

**Volumes** provide the ability to connect specific filesystem paths of the container back to the host machine.

Before your computer can use any kind of storage device (such as a hard drive, CD-ROM, or network share), you or your operating system must make it accessible through the computer's file system. This process is called **mounting**.

If a directory in the container is mounted, changes in that directory are also seen on the host machine. If we mount that same directory across container restarts, we'd see the same files.

- Create a volume, using `docker volume create [Name]`
