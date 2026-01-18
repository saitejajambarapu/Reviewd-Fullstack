Reviewed – Fullstack Movie Review Platform 🎬

Reviewed is a fullstack movie browsing + review platform inspired by IMDb/Letterboxd.
Users can search movies/series using IMDb/OMDb data, view content details, rate items, add reviews, like/watchlist content, and interact with community reviews.

This project was built to practice Full Stack Development including:

Spring Boot backend + MySQL

React frontend

Docker containerization

Kubernetes deployment (GKE / any cluster)

Features

Search movies/series using IMDb Id

Fetch content details using IMDb/OMDb API

View complete movie details: title, plot, cast, genre, rating, etc.

Like / Watchlist content

Add rating (1–10 stars)

Write reviews

View similar reviews (recommendation section)

Fallback image (Alt poster) when poster is missing/broken

Notification system (frontend)

Deployed using Docker + Kubernetes

Tech Stack
Frontend

React JS

React Router

Axios

Material UI (Popover etc.)

Custom CSS

Backend

Java 17+

Spring Boot

Spring Security

Spring Data JPA (Hibernate)

MySQL

DevOps

Docker

Docker Compose

Kubernetes (kubectl, deployments, services)

(Optional: GKE Autopilot)

External API Used

This project uses IMDb/OMDb API to fetch movie/series details.

Example call pattern:

GET /content/imdb?imdbId=tt#######


Backend calls OMDb/IMDb API and stores/interacts with MySQL.

Project Structure (Example)
Reviewed-Fullstack/
 ├── backend/                # Spring Boot backend
 ├── frontend/               # React frontend
 ├── k8s/                    # Kubernetes YAML manifests
 ├── docker-compose.yml
 └── README.md

Setup Instructions
1) Run using Docker Compose (Local)

Start all services:

docker compose up -d


Check running containers:

docker ps


Stop:

docker compose down

2) Run Frontend locally
cd frontend
npm install
npm start

3) Run Backend locally
cd backend
mvn clean install
mvn spring-boot:run

MySQL Init / Insert Commands
Enter MySQL inside Docker container
docker exec -it reviewed-mysql mysql -uroot -p


Then:

USE reviewed;
SELECT * FROM home_page_sections_entity;


(Insert queries used for homepage sections are stored in the SQL file / documentation.)

Kubernetes Deployment
Check deployments
kubectl get deployments -n reviewed

Check pods
kubectl get pods -n reviewed

Update Frontend Image in Kubernetes
Push frontend Docker image
docker build -t saitejajambarapu/reviewed-frontend:1.0 .
docker push saitejajambarapu/reviewed-frontend:1.0

Apply image in deployment
kubectl set image deployment/frontend frontend=saitejajambarapu/reviewed-frontend:1.0 -n reviewed

Restart frontend deployment
kubectl rollout restart deployment/frontend -n reviewed
kubectl rollout status deployment/frontend -n reviewed

Verify frontend build output inside Kubernetes
kubectl exec -n reviewed deploy/frontend -- ls -l /usr/share/nginx/html

Commands Used (Quick Reference)
Docker commands
docker ps -a
docker images
docker build -t saitejajambarapu/reviewed-frontend:1.0 .
docker push saitejajambarapu/reviewed-frontend:1.0
docker pull saitejajambarapu/reviewed-frontend:1.0
docker rmi <image>
docker rm <container>

Kubernetes commands
kubectl get deployments -n reviewed
kubectl get pods -n reviewed
kubectl set image deployment/frontend frontend=saitejajambarapu/reviewed-frontend:1.0 -n reviewed
kubectl rollout restart deployment/frontend -n reviewed
kubectl rollout status deployment/frontend -n reviewed
kubectl exec -n reviewed deploy/frontend -- ls -l /usr/share/nginx/html
kubectl describe deployment frontend -n reviewed


Author
Sai Teja Jambarapu
Fullstack Developer | Spring Boot | React | Kubernetes | AWS
