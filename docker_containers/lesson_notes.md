# Notes to be organised & assorted


## Volumes & Persistance



############################################################################

#### Persistance
Containers have so far effectively been 'Read Only'. Changes isolated to a removed container will be lost.

**Volumes** provide the ability to connect specific filesystem paths of the container back to the host machine.

Before your computer can use any kind of storage device (such as a hard drive, CD-ROM, or network share), you or your OS must make it accessible through the computer's file system. This process is called **mounting**.

If a directory in the container is mounted, changes in that directory are also seen on the host machine. If we mount that same directory across container restarts, we'd see the same files.

- Create a volume, using `docker volume create [Name]`
