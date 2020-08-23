FROM openfaas/of-watchdog:0.8.0 AS watchdog
FROM alpine:3.10 AS ship

COPY --from=watchdog /fwatchdog /usr/bin/fwatchdog
RUN chmod +x /usr/bin/fwatchdog

WORKDIR /home/app
COPY ./function/static .

ENV mode="static"
ENV static_path="/home/app"

HEALTHCHECK --interval=3s CMD [ -e /tmp/.lock ] || exit 1

CMD ["fwatchdog"]
