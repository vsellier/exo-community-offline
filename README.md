# eXo Community - Offline example


## Prepare the image

On a server havine internet access :

### Customize the installation

#### Via the example
Clone the repository
```
# git clone https://github.com/vsellier/exo-community-offline.git
# cd exo-community-offline
```
and customize the ``Dockerfile`` file to install your specific addons

#### From scratch

```
# mkdir exo-community-offline
# vi Dockerfile
```

```
FROM exoplatform/exo-community:5.0

RUN ./addon install <addon>
RUN ./addon install <addon>
...
```

### Build the image

```
# docker build -t exo-community-offline .
```

### Transfer the image

If the image preparation can't be done on the server running eXo platform, you will have to export the prepared image to the targer server

#### Export the image

On the same server the build was done :

```
# docker save -o exo-community-offline.tar exo-community-offline
```

and transfer the tar file to the offline server

#### Import the image

On the server with no internet access

(i) you must have transferred the previous exported image onto this server

```
# docker load -i exo-community-offline.tar
```

## Run the image

The prepared image can be now run as the official [eXo community image](https://github.com/exo-docker/exo-community)
just replacing the image name by ``exo-community-offline```:

```
# docker run -v exo_data:/srv/exo -p 8080:8080 exo-community-offline
```

See [eXo community project page](https://github.com/exo-docker/exo-community) for more information on how to configure an eXo community instance.