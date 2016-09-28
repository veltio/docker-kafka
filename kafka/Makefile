all: build

clean:
	@docker stop kafka && docker rm kafka

build:
	@docker build --rm=false --tag=veltio/kafka .

test:
	build
	@docker run --name='kafka' \
	-it \
	--rm \
	-p 9092:9092 \
	-p 2181:2181 \
	-v /var/run/docker.sock:/var/run/docker.sock \
	-v $$(which docker):/bin/docker \
	veltio/kafka

run:
	@docker run --name='kafka' \
        -d \
	-e "LOG_CLEANER_ENABLE=true" \
	-e "LOG_RETENTION_HOURS=24" \
	-p 9093:9093 \
	-p 2182:2182 \
	-v /Users/gsilva/kafka:/var/kafka \
	-v /var/run/docker.sock:/var/run/docker.sock \
	-v $$(which docker):/bin/docker \
	veltio/kafka

logs:
	@docker logs -f kafka
