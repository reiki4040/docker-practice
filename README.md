sample docker logger and docker-compose
===

run docker images that webapp and fluentd docker with docker-compose.

- golang webapp that scratch base.
- collect stdout/err logs and forward with fluentd logger.
- fluentd receive log from fluentd logger and output to stdout.

## command

ship containers

```
docker-compose up -d
```

tail fluentd container logs

```
docker logs -f docker_fluentd_1
```

maybe shown fluentd startup logs (configuration and listen port...)

access webapp

```
curl https://{docker-machine ip}:8000/api/hello
```

then shown webapp logs (example)

```
2016-07-23 09:56:20 +0000 docker.3e8a437d25caa93d4d29f52592c1be4ac08a7d5b7360431b3759f2f9180a575b: {"container_id":"3e8a437d25caa93d4d29f52592c1be4ac08a7d5b7360431b3759f2f9180a575b","container_name":"/docker_goweb-comp_1","source":"stderr","log":"2016/07/23 09:56:20.970989 Starting Goji on [::]:8000"}
2016-07-23 09:56:35 +0000 docker.3e8a437d25caa93d4d29f52592c1be4ac08a7d5b7360431b3759f2f9180a575b: {"source":"stderr","log":"2016/07/23 09:56:35.120381 [3e8a437d25ca/sv2XrTFI1V-000001] Started GET \"/api/hello\" from 192.168.99.1:50020","container_id":"3e8a437d25caa93d4d29f52592c1be4ac08a7d5b7360431b3759f2f9180a575b","container_name":"/docker_goweb-comp_1"}
2016-07-23 09:56:35 +0000 docker.3e8a437d25caa93d4d29f52592c1be4ac08a7d5b7360431b3759f2f9180a575b: {"log":"logging my middleware start.","container_id":"3e8a437d25caa93d4d29f52592c1be4ac08a7d5b7360431b3759f2f9180a575b","container_name":"/docker_goweb-comp_1","source":"stdout"}
2016-07-23 09:56:35 +0000 docker.3e8a437d25caa93d4d29f52592c1be4ac08a7d5b7360431b3759f2f9180a575b: {"container_id":"3e8a437d25caa93d4d29f52592c1be4ac08a7d5b7360431b3759f2f9180a575b","container_name":"/docker_goweb-comp_1","source":"stdout","log":"logging my middleware end."}
2016-07-23 09:56:35 +0000 docker.3e8a437d25caa93d4d29f52592c1be4ac08a7d5b7360431b3759f2f9180a575b: {"log":"2016/07/23 09:56:35.120756 [3e8a437d25ca/sv2XrTFI1V-000001] Returning 200 in 143.439µs","container_id":"3e8a437d25caa93d4d29f52592c1be4ac08a7d5b7360431b3759f2f9180a575b","container_name":"/docker_goweb-comp_1","source":"stderr"}
```
