## <a name="_oj8c4cubvmn9"></a>Task 2: Deploy nginx container
1. Nginx container - deploy using host networking
1. Nginx container - deploy using port mapping
### <a name="_wx1l01h548ek"></a>Assessment
Accessing http://localhost:8000 should display the “Welcome to Nginx page”.
### <a name="_degmqzkzcwee"></a>Learning Outcomes
1. Understanding the different deployment options for Nginx containers: host networking and port mapping.
1. Familiarity with container networking concepts and their impact on container accessibility.

```
 docker pull nginx
```
```
 docker run -d --name task -p 8080:80 nginx
```
