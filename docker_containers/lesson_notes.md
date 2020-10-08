# Notes to be organised & assorted


## Volumes & Persistence
Containers have so far effectively been 'Read Only'. Changes isolated to a removed container will be lost.

- **Persistent** = Data that is to be stored - eg user credentials / sales figures.
- **Non-persistent** = Data that is unwanted after it has fulfilled its use.

**Volumes** provide the ability to connect specific filesystem paths of the container back to the host machine.

Before your computer can use any kind of storage device (such as a hard drive, CD-ROM, or network share), you or your OS must make it accessible through the computer's file system. This process is called **mounting**.

Containers are good at handling _non-persistent_ and _ephemeral_ data, and tend to be short-lived
Once it has completed its task, it stops and the data within is generally lost.
If we want to change a container, we create a new one and add.

Volumes store persistent data. They are directories, stored elsewhere, that can be mounted directly onto a container.

When editing a volume from within a container (already mounted), the data will become persistent and remain in the volume even after the container has been removed.

A volume *cannot* be deleted if in use on another container.


## Secrets
