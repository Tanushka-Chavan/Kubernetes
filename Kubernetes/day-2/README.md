# 📅 Day 2 – From “It Works on My Machine” to Docker 🐳

Today was the day things finally started clicking.
Not just watching tutorials… but actually *building, breaking, fixing, and running things myself*.

---

## 🚀 What I did today

* Picked up a sample Node.js app
* Turned it into a Docker container
* Built my own Docker image
* Pushed it to Docker Hub 🌍
* Pulled it back and ran it like a real app

---

## 📥 Started with a project

git clone https://github.com/docker/getting-started-app.git
cd getting-started-app

Instead of writing code from scratch, I used this app to focus purely on understanding Docker.

---

##⚙️ Dockerfile Breakdown

FROM node:18-alpine → Lightweight Node.js environment

WORKDIR /app → Sets working directory inside container

COPY . . → Copies project files

RUN npm install --production → Installs required dependencies

CMD ["node","src/index.js"] → Runs the application

EXPOSE 3000 → Defines the app port


---

## ⚙️ What each line does (in simple terms)

* FROM node:18-alpine → gives my app a lightweight environment to run
* WORKDIR /app → sets up a workspace inside the container
* COPY . . → moves my project files into the container
* RUN npm install --production → installs only what’s needed
* CMD ["node","src/index.js"] → tells the container how to start the app
* EXPOSE 3000 → lets Docker know which port the app uses

---

## 🏗️ Built the image

docker build -t day2 .

This is where my project stopped being “just code” and became a **Docker image**.

---

## 🏷️ Tagged the image

docker tag day2:latest tanushka28/latest-repo:latest

Gave my image a proper name so it can live on Docker Hub.

---

## ☁️ Docker Hub steps

1. Created a repository (latest-repo) on Docker Hub
2. Logged in from terminal

docker login

3. Pushed the image

docker push tanushka28/latest-repo:latest

Now my image isn’t just on my laptop… it’s available online.

---

## 📥 Pulled the image

docker pull tanushka28/latest-repo:latest

Pulled it back just to make sure everything works from anywhere.

---

## ▶️ Ran the container

docker run -dp 3000:3000 tanushka28/latest-repo:latest

* -d → runs in background
* -p → connects my system to the container

---

## 🔎 Checked containers

docker ps
docker ps -a
docker logs <container_id>

Used these to see what’s running and what’s actually happening inside.

---

## 🎯 End of Day

This didn’t feel like just another practice session.

It felt like:

* I built something real ✅
* I shared it online ✅
* I ran it like an actual application ✅

---

## 💭 Takeaway

Docker isn’t just a tool…
it’s what makes your app **portable, shareable, and production-ready**.

---

## 🔥 Highlight

Seeing my image on Docker Hub made me pause for a second:

“Wait… this can literally run anywhere now.”

And that felt pretty cool 😄

---

# ☸️ Deploying the Same App on Kubernetes

After building and pushing the Docker image, I took the next step — running it on Kubernetes 🚀

---

## 📦 Docker Image Used

ghcr.io/tanushka-chavan/day2-final:latest

---

## 📄 Deployment Configuration

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: day2-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: day2-app
  template:
    metadata:
      labels:
        app: day2-app
    spec:
      containers:
        - name: day2-container
          image: ghcr.io/tanushka-chavan/day2-final:latest
          ports:
            - containerPort: 3000
```

---

## 📄 Service Configuration

```yaml
apiVersion: v1
kind: Service
metadata:
  name: day2-service
spec:
  type: NodePort
  selector:
    app: day2-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 3000
      nodePort: 30007
```

---

## 🚀 Run on Kubernetes

kubectl apply -f deployment.yaml
kubectl apply -f service.yaml

---

## 🌐 Access the App

minikube service day2-service

---

## 📊 Verify

kubectl get pods
kubectl get svc

---

## 🎯 Final Thought

What started as:
👉 “It works on my machine”

Turned into:
👉 “It runs anywhere — Docker + Kubernetes”

That shift… is what makes DevOps powerful 💥
