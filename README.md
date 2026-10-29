# Experiment 11: Containerizing and Executing a Java or Python Application Using Docker

- **Student Name**: Sharma Shubh
- **USN**: 4NI25CS191
- **Semester / Section**: 3rd Sem, Sec-G
- **Course**: Collaborative Development and DevOps (1BCS303)
- **Institution**: The National Institute of Engineering, Mysuru

---

## 1. Aim
To containerize and execute a simple Java or Python application using Docker by creating a Dockerfile, building a Docker image, running a container, and verifying the application output.

---

## 2. Files in Repository
- `app.py`: Simple Python arithmetic program executing basic sum operations.
- `Dockerfile`: Multi-layer Dockerfile packaging Python 3.12 runtime and script.
- `.dockerignore`: Excludes `.git`, `__pycache__`, and `*.pyc` from build context.

---

## 3. Commands & Terminal Output

### Step 1 & 2: Author Application Code (`app.py`)
```python
print("Welcome to Docker Lab!")
print("Python application is running inside a container.")

a = 10
b = 20
result = a + b

print("First number:", a)
print("Second number:", b)
print("Sum:", result)
```

### Step 3: Author Dockerfile
```dockerfile
FROM python:3.12-slim
WORKDIR /app
COPY app.py .
CMD ["python", "app.py"]
```

### Step 4: Build Docker Image
```bash
$ docker build -t python-app .
[+] Building 4.8s (8/8) FINISHED
 => [1/3] FROM docker.io/library/python:3.12-slim
 => [2/3] WORKDIR /app
 => [3/3] COPY app.py .
 => naming to docker.io/library/python-app
```

### Step 5: Verify Local Image
```bash
$ docker images
REPOSITORY   TAG       IMAGE ID       CREATED          SIZE
python-app   latest    3c8e9f1a2b4d   10 seconds ago   128MB
```

### Step 6: Run Container
```bash
$ docker run --name python-container python-app
Welcome to Docker Lab!
Python application is running inside a container.
First number: 10
Second number: 20
Sum: 30
```

### Step 7: Inspect Container Lifecycle & Logs
```bash
$ docker ps -a
CONTAINER ID   IMAGE        COMMAND           STATUS                     NAMES
4f2b1a8c9e0d   python-app   "python app.py"   Exited (0) 15 seconds ago  python-container

$ docker logs python-container
Welcome to Docker Lab!
Python application is running inside a container.
First number: 10
Second number: 20
Sum: 30
```

### Step 8: Re-run Existing Container
```bash
$ docker start -a python-container
Welcome to Docker Lab!
Python application is running inside a container.
First number: 10
Second number: 20
Sum: 30
```

### Step 9: Clean Up Container and Image
```bash
$ docker rm python-container
python-container

$ docker rmi python-app
Untagged: python-app:latest
Deleted: sha256:3c8e9f1a2b4d...
```

---

## 4. Result
A simple Python application was authored, packaged into a Docker image using a custom Dockerfile, executed inside an isolated container, and verified through stdout logs and lifecycle status checks.
