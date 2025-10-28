## Project Structure
<img width="206" height="250" alt="image" src="https://github.com/user-attachments/assets/2904e648-bf52-4696-98c0-04965300a4b2" />

## Step-1: Build the Docker Images for Each Application

#### Homepage
HERE we are building the homepage-v2 Image which include -> Games Page for our Movieflix Application

### Befor that we need to edit nginx.conf
Add the games path in our existing nginx.conf file
```
        location /games/ {
            proxy_pass http://games-app:80/;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
        }
```

## Build the hopmepage-v2 Image

cd homepage
```
docker build -t sapsecops/movieflix-micro:homepageV2 .
```

#### Build Movies App Image
cd movies
```
docker build -t sapsecops/movieflix-micro:moviesV1 .
```

#### Build songs App Image
cd songs
```
docker build -t sapsecops/movieflix-micro:songsV1 .
```

#### Build games App Image
cd games
```
docker build -t sapsecops/movieflix-micro:gamesV1 .
```

## Step-2: Create private Docker network for our Movieflix Application

##### To connect containers without IPs, use a bridge network:
```
docker network create movieflix-network
```


## Step-3: Run the Container 

Here we are using Microservice Application, in nginx.conf we use reverse proxy to the movies-app, songs-app, games-app

So first we need to Launch that Applications --> Later we Deploy the Homepage Application

##### Run the Movies App Container
```
docker run -d --name movies-app --network movieflix-network sapsecops/movieflix-micro:moviesV1
```

##### Run the Songs App Container
```
docker run -d --name songs-app --network movieflix-network sapsecops/movieflix-micro:songsV1
```

##### Run the Homepage App Container
```
docker run -d --name homepage --network movieflix-network -p 80:80 sapsecops/movieflix-micro:homepageV2
```