# Working with Images

An image is a read only template of stacked layers used for creating application containers.

These layers are independent, and only loosely connected through the accompanying manifest (config) file.
- Base layer (OS)
- (App layer)
- (Update layer)
- (etc...)

Image ID is a hash of image config file

Layers are referenced via hashing - content hashing

They contain a JSON manifest, code and supporting files to build an app.

Images stored on a registry (Cloud or on-prem) and pulled to host using `docker image pull ... (-a)`.

Pushed to repo using `docker image push ...`.

When a container is created from an image, a writable layer is added.

To show config and layers of an image, use `docker image inspect ...`

To delete, use `docker image rm ...`

### Registries

Image storage, eg Dockerhub (official)

Unofficial repos can be created by any person or organisation - stick to using official where possible

When pushing and pulling from repos, images are compressed using hashing / digests
- Compressed (when pushing) using distribution hashes
- Uncompressed using content hashes
