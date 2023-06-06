
# Use this to control building and pushing of Docker images in a significantly less ugly fashion.
#

# Top level Makefile commands (also can build individual images with `make build-<server|daemons|webui|etc...>`)
push-all:
	$(push-fts3-cmd)
	$(push-gridcerts-cmd)

build-all:
	$(build-fts3-cmd)
	$(build-gridcerts-cmd)

build-all-nc:
	$(build-fts3-nc-cmd)
	$(build-gridcerts-nc-cmd)

# Image build command definitions
define build-fts3-cmd =
podman build --label "maintainer=$(whoami)" -t rubin-fts3 fts3
endef

define build-fts3-nc-cmd =
podman build --label "maintainer=$(whoami)" --no-cache -t rubin-fts3 fts3
endef

define build-gridcerts-cmd =
podman build --label "maintainer=$(whoami)" -t grid-security-files grid-certificates
endef

define build-gridcerts-nc-cmd =
podman build --label "maintainer=$(whoami)" --no-cache -t grid-security-files grid-certificates
endef

# Image build command declarations
build-fts3:
	$(build-fts3-cmd)

build-fts3-nc:
	$(build-fts3-nc-cmd)

build-gridcerts:
	$(build-gridcerts-cmd)

build-gridcerts-nc:
	$(build-gridcerts-nc-cmd)

# Image push command definitions
define push-fts3-cmd =
	podman tag rubin-fts3 bjwhitefnal/rubin-fts3:${RUBIN_FTS3_VERSION}
	podman push bjwhitefnal/rubin-fts3:${RUBIN_FTS3_VERSION}
endef

define push-gridcerts-cmd =
	podman tag grid-security-files bjwhitefnal/grid-security-files:latest
	podman push bjwhitefnal/grid-security-files:${RUBIN_FTS3_VERSION}
endef

# Image push command declarations
push-fts3:
	$(push-fts3-cmd)

push-gridcerts:
	$(push-gridcerts-cmd)
