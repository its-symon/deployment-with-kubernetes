# Movie Management System API — Docker & Kubernetes Deployment

This project demonstrates how I containerized a Django API application and deploy it on a local Kubernetes cluster using **Docker**, **Docker Hub**, and **Minikube**.

---

## What I Did

1. **Containerized the Django Application**  
   Created a `Dockerfile` and built a Docker image for the Django backend.

2. **Pushed Image to Docker Hub**  
   Tagged and pushed the image to my Docker Hub account:
   ```bash
    docker tag movie_app itssymonbarua640/movie_app
    docker push itssymonbarua640/movie_app
   ```

3. **Created Kubernetes Pod**  
Defined a `Pod` manifest (`runpod.yml`) using the Docker image from Docker Hub.

4. **Exposed the Pod Using a Service**  
Used a Kubernetes `Service` of type `NodePort` to expose the Django app externally:
```bash
kubectl expose pod movie-pod --name=django-svc --type=NodePort --port=8000 --target-port=8000
```

5. **Accessed the App via Minikube Tunnel**  
Since I'm on macOS using the Docker driver, I accessed the app using:
``` minikube service django-svc ```



---

## 📁 Files in This Project

- `Dockerfile`: Container configuration for the Django app
- `requirements.txt`: Python dependencies
- `runpod.yml`: Kubernetes Pod configuration

---

## 🧠 Notes

- On macOS (Docker driver), direct access via `NodePort` (like `http://192.168.x.x:<port>`) doesn't work.
- Instead, I used:
```bash
  minikube service django-svc 
```



## 🔧 Commands Summary

### Docker

```bash
docker build -t movie_app .
docker tag movie_app itssymonbarua640/movie_app
docker push itssymonbarua640/movie_app
```

### Kubernetes
``` bash
kubectl apply -f runpod.yml
kubectl expose pod movie-pod --name=django-svc --type=NodePort --port=8000 --target-port=8000
minikube service django-svc
```


## Author 
Symon
Author
Learning Docker + Kubernetes — One Pod at a Time 🚢☸️