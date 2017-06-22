VOL_MOUNT = -v $(shell pwd):/src
IMAGETAG = trezor-prod-test

all: .wrap

.wrap: .docker-image
	docker run -i -t $(VOL_MOUNT) $(IMAGETAG) /bin/sh -c 'cd /src ; make build'

build:
	i686-w64-mingw32-gcc test-trezor.c -Wl,-Bstatic -lhidapi -Wl,-Bdynamic -lsetupapi -mwindows -o test-trezor-32bit.exe
# /usr/i686-w64-mingw32/sys-root/mingw/lib/libhidapi.a

.docker-image:
	$(info Preparing docker image ...)
	docker build -t $(IMAGETAG) .

shell: .docker-image
	docker run -i -t $(VOL_MOUNT) $(IMAGETAG) /bin/bash