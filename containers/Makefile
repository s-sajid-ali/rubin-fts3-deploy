
# Use this to control building and pushing of Docker images in a significantly less ugly fashion.
#

# Top level Makefile commands (also can build individual images with `make build-<server|daemons|webui|etc...>`)
push-all:
	$(push-fts3-cmd)

build-all:
	$(build-fts3-cmd)

build-all-nc:
	$(build-fts3-nc-cmd)

# Image build command definitions
define build-fts3-cmd =
docker build --label "maintainer=$(whoami)" -t rubin-fts3 fts3
endef

define build-fts3-nc-cmd =
docker build --label "maintainer=$(whoami)" --no-cache -t rubin-fts3 fts3
endef

# Image build command declarations
build-fts3:
	$(build-fts3-cmd)

build-fts3-nc:
	$(build-fts3-nc-cmd)

# Image push command definitions
define push-fts3-cmd =
	docker tag rubin-fts3 bjwhitefnal/rubin-fts3:${RUBIN_FTS3_VERSION}
	docker push bjwhitefnal/rubin-fts3:${RUBIN_FTS3_VERSION}
endef

# Image push command declarations
push-fts3:
	$(push-fts3-cmd)
