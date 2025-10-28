## Project Structure
<img width="206" height="250" alt="image" src="https://github.com/user-attachments/assets/2904e648-bf52-4696-98c0-04965300a4b2" />

## Step-1: Build the Docker Images for Each Application

#### Homepage
cd homepage
```
docker build -t sapsecops/movieflix-micro:homepageV1 .
```

#### Movies
cd movies
```
docker build -t sapsecops/movieflix-micro:moviesV1 .
```

#### Songs
cd songs
```
docker build -t sapsecops/movieflix-micro:songsV1 .
```

## Step-2: Create private Docker network for our Movieflix Application

##### To connect containers without IPs, use a bridge network:
```
docker network create movieflix-network
```


## Step-3: Run the Container 

##### Run the Homepage App Container
```
docker run -d --name homepage --network movieflix-network -p 80:80 sapsecops/movieflix-micro:homepageV1
```

##### Run the Movies App Container
```
docker run -d --name movies-app --network movieflix-network sapsecops/movieflix-micro:moviesV1
```

##### Run the Songs App Container
```
docker run -d --name songs-app --network movieflix-network sapsecops/movieflix-micro:songsV1
```