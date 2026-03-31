ENTRYPOINT=main.ts
DENO_PERMISSIONS=--allow-net --allow-env --allow-read --allow-write

DENO_FREEZE ?= true

run: fontgen
	cd ../scripts; \
		npm install; \
		npm run buildLib
	deno run $(DENO_PERMISSIONS) $(ENTRYPOINT)

check:
	deno check $(ENTRYPOINT)

fontgen:
	deno run --allow-read --allow-write --frozen=$(DENO_FREEZE) fontgen.ts

test: fontgen check
	deno test --allow-env --allow-read --allow-net --allow-write --allow-run --frozen=$(DENO_FREEZE) test.ts

build: fontgen check
	deno run --allow-env --allow-read --allow-net --allow-write --allow-run --frozen=$(DENO_FREEZE) bundle.ts

install: build
	deno install $(DENO_PERMISSIONS) -f -n fabric bundled.ts

install-bundled: build
	deno install $(DENO_PERMISSIONS) -f -n fabric bundled.ts

init:
	rm -rf ./test
	deno run $(DENO_PERMISSIONS) $(ENTRYPOINT) init ./test

init-bundled: build
	rm -rf ./test
	deno run $(DENO_PERMISSIONS) bundled.ts init ./test
