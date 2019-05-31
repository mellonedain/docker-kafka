kafka_version=0.10.1.1

run:
	docker run -it -p 2181:2181 -p 9092:9092 --name kafka docker.io/mellonedain/kafka:latest

build:
	docker build -t docker.io/mellonedain/kafka:latest .
	docker build -t docker.io/mellonedain/kafka:$(kafka_version) .

push:
	docker push docker.io/mellonedain/kafka:latest
	docker push docker.io/mellonedain/kafka:$(kafka_version)

