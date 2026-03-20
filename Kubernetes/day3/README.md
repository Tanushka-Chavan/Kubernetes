# 📅 Day 3 – Optimizing with Multi-Stage Builds ⚡

After successfully building and running my first Docker image,
today I focused on making it **smaller, cleaner, and production-ready** using multi-stage builds.

---

## 🚀 What I did today

* Cloned a sample React-based Todo App
* Created a multi-stage Dockerfile
* Built the application in one stage
* Served it using Nginx in another stage
* Fixed multiple Dockerfile errors along the way 😄

---

## 📥 Project Setup

```bash
git clone https://github.com/piyushsachdeva/todoapp-docker
cd todoapp-docker
```

---

## 🧾 Multi-Stage Dockerfile

```dockerfile
# ---------- Stage 1: Build ----------
FROM node:18 AS installer

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

RUN npm run build


# ---------- Stage 2: Production ----------
FROM nginx:latest

COPY --from=installer /app/build /usr/share/nginx/html
```

---

## ⚙️ How it works

### 🔹 Stage 1 (Builder)

* Uses Node.js to install dependencies
* Builds the React app
* Generates optimized static files

### 🔹 Stage 2 (Production)

* Uses Nginx (lightweight web server)
* Copies only the final build output
* No unnecessary dependencies included

---

## 🏗️ Build the Image

```bash
docker build -t multi-stage .
```

---

## ▶️ Run the Container

```bash
docker run -dp 3000:80 multi-stage
```

* `-d` → run in background
* `-p 3000:80` → map local port to container port

👉 Open in browser:
http://localhost:3000

---

## 📊 Verify

```bash
docker ps
docker images
```

---


## 🎯 Key Learning

Multi-stage builds help to:

* Reduce image size 📉
* Improve performance ⚡
* Remove unnecessary files 🧹
* Keep images production-ready 🚀

---

## 💭 Takeaway

Earlier, my Docker image contained everything — including unnecessary files and dependencies.

Now, with multi-stage builds, it only contains what is required to run the app.

That’s a big step towards writing **efficient and optimized Dockerfiles**.

---

## 🔥 Highlight

Understanding that:

> “Build environment and runtime environment don’t have to be the same”

was a real game changer today 🚀
