## Build the image
```
docker build -t sapsecops/movieflix-mono:v1 .
```
## Run the container
```
docker run -d -p 80:80 --name movieflix-mono sapsecops/movieflix-mono:v1
```

## Push Image to the Registry
```
docker push sapsecops/movieflix-mono:v1 .
```
