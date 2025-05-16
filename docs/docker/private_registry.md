# private registry 
1. login to registry
```
docker login private-registry.io
```
2. run the app
```
docker run private-registry.io/interal-app
```
3. Deploy Private Registry
```
docker run -d -p 5000:5000 --restart always --name registry registry:2
```
4. create image
```
docker image tag my-image localhost:5000/my-image
```
5. pull image
```
docker pull localhost:5000/my-image
```
6. push image
```
docker push localhost:5000/my-image
```
7. verify image
```
curl -X GET localhost:5000/v2/_catalog
```
