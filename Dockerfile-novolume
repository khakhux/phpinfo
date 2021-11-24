FROM alpine:latest AS multilayer
RUN apk add php
COPY index.php src/index.php

FROM scratch AS singlelayer
COPY --from=multilayer / /
