# scicat_k8s
This project contains manifests that support the production version of SciCat at ALS. This will hopefully turn into a helm repository in the future (which is why the manifests are in the `templates` folder.

SciCat is a mulifacility project. It's repos require some amount of override-through-volume-mounts to make customizations when using their published container images. In order to maintain ALS customizations and have them constantly pulled from git, the frontend and app deployments contain (well, currently, just the app deployment for now) the SciCat backend as well as a git-sync initContainers sidecar. When the sidecar starts up, it syncs with the [scicat_als_config](https://github.com/als-computing/scicat_als_config.git) repo, where we maintain our customization files. It then uses an emptyDir k8s volume which is shared with the app. The app mounts files and directories from that mount.

