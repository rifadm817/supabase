FROM kong/kong:3.9.1
USER root
COPY ./kong.yml /home/kong/temp.yml
COPY --chmod=777 ./kong-entrypoint.sh /home/kong/kong-entrypoint.sh
# The base image ends with `USER kong`, but /home/kong does not exist in it, so
# the COPY above creates it as root:root 0755. The entrypoint runs as `kong` and
# writes $KONG_DECLARATIVE_CONFIG (/home/kong/kong.yml), which fails with
# "Permission denied" unless the directory is owned by the kong user.
RUN chown -R kong:0 /home/kong && chmod -R g+rwX /home/kong
USER kong
ENTRYPOINT ["/bin/sh", "/home/kong/kong-entrypoint.sh"]
