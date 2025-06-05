## <a name="_o45zpox401a2"></a>Task 3: Nginx static file serving
1. Use nginx to serve static files from the host
### <a name="_99ql8yvqahxd"></a>Assessment
Accessing http://localhost:8000/welcome.html should display the provided html page.
### <a name="_oiymls13p7qz"></a>Learning Outcomes
1. Mapping external data sources into docker containers.
1. Containers are non-persistent

```
docker run -v "$PWD":/usr/share/nginx/html:ro -p 8080:80 -d nginx
```
