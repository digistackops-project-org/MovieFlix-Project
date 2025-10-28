## Build the image
docker build -t movieflix-mono:v1 .

## Run the container
docker run -d -p 80:80 --name movieflix-mono movieflix-mono:v1
