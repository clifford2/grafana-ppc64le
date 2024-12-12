# Grafana container for ppc64le

This was a container build of [Grafana](https://grafana.com/) for **ppc64le** systems.

**It is no longer maintained**.

These builds use the source code from <https://github.com/grafana/grafana>.

At the moment, only **v7.0.5** is available.

To build this for `ppc64le`, I made the following minor changes to the `Dockerfile`:

```diff
--- a/Dockerfile
+++ b/Dockerfile
@@ -1,5 +1,7 @@
 FROM node:12.16.3-alpine3.11 as js-builder
 
+RUN apk add python make g++
+
 WORKDIR /usr/src/app/
 
 COPY package.json yarn.lock ./
@@ -68,7 +70,7 @@ RUN mkdir -p "$GF_PATHS_HOME/.aws" && \
     chown -R grafana:grafana "$GF_PATHS_DATA" "$GF_PATHS_HOME/.aws" "$GF_PATHS_LOGS" "$GF_PATHS_PLUGINS" "$GF_PATHS_PROVISIONING" && \
     chmod -R 777 "$GF_PATHS_DATA" "$GF_PATHS_HOME/.aws" "$GF_PATHS_LOGS" "$GF_PATHS_PLUGINS" "$GF_PATHS_PROVISIONING"
 
-COPY --from=go-builder /go/src/github.com/grafana/grafana/bin/linux-amd64/grafana-server /go/src/github.com/grafana/grafana/bin/linux-amd64
+COPY --from=go-builder /go/src/github.com/grafana/grafana/bin/linux-ppc64le/grafana-server /go/src/github.com/grafana/grafana/bin/linux-ppc
 COPY --from=js-builder /usr/src/app/public ./public
 COPY --from=js-builder /usr/src/app/tools ./tools
```

The modified file is available in `Dockerfile-v7.0.5-ppc64le`.

## Docker Hub Images

Built images are no longer available.

For usage instructions, see <https://grafana.com/docs/grafana/latest/installation/docker/>.
