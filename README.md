# Project : Streamlined Web Application Deployment using Docker, AWS, Nginx, and

## Using Docker

### Application Requirements
- Source code
- Runtime (Node.js)
- Dependencies

> A container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another.

> It uses a **Container Image** that packages up the complete application.

## Virtual Machines vs Containers

| Feature              | Virtual Machines          | Containers               |
|----------------------|---------------------------|--------------------------|
| Startup Time         | Minutes to start          | Seconds to start         |
| Resource Overhead    | Higher overhead           | Lower overhead           |
| Portability          | Limited portability       | High portability         |
| Scalability          | Moderate scaling          | Rapid scaling            |
| Management           | More complex              | Simplified management    |
| Performance          | Performance overhead      | Near-native performance  |
| Maintenance          | Heavy maintenance         | Easy maintenance         |
| Isolation            | Strong isolation          | Lightweight isolation    |

## Setup an EC2 Instance

- **OS**: Ubuntu 24.04  
- **Instance Type**: t2.medium  

### Steps

1. Install Docker
2. Clone git repository  
   ```bash
   git clone <repo-url>
   ```
3. Build Docker image  
   ```bash
   docker build -t wedding-image .
   ```
4. List images  
   ```bash
   docker images
   ```
5. Run container  
   ```bash
   docker run -d -p 80:80 wedding-image
   ```
6. Check running containers  
   ```bash
   docker ps
   ```
7. Access application  
   `http://<public-ip>:80`  
   Example: `http://142.93.17.12:80`

8. Enter container (optional)  
   ```bash
   docker exec -it <container_id> /bin/bash
   ```

9. Stop container  
   ```bash
   docker stop <container_id>
   ```

**Finished ..!**
```
