all: build test

build: . logs temp
	gofmt -w .
	go build -o .\temp .

mockery:
	mockery --dir repository --all

test: mockery logs
	go test -v -coverprofile=logs/c.out -coverpkg ./models/ ./...
	go tool cover -html=logs/c.out -o logs/coverage.html 

run: build
	.\temp\gateway.exe

docker-push:
	docker build --no-cache -t fairay/rsoi-lab4-gateway .
	docker push fairay/rsoi-lab4-gateway:latest

# Creating directories
DIRS?=logs temp
$(DIRS):
	mkdir -p $@
