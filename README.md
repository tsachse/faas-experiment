# OpenFaas-Experiment

## openfaas

https://github.com/openfaas/faas
https://github.com/openfaas/faas-cli

````
export MINIO_SECRET_KEY=vMIoCaBu9sSg4ODrSkbD9CGXtq0TTpq6kq7psLuE
export MINIO_ACCESS_KEY=ZBPIIAOCJRY9QLUVEHQO

./deploy_stack.sh

faas-cli build -f ./colorize.yml
faas-cli deploy -f ./colorize.yml
faas-cli remove -f ./colorize.yml
`````
## minio

https://github.com/minio/minio
https://github.com/minio/mc



## Colourising Video with OpenFaaS Serverless Functions

https://finnian.io/blog/colourising-video-with-openfaas-serverless-functions/
https://github.com/developius/repaint-the-past

````
mc config host add minio http://tsachse720:9000 ZBPIIAOCJRY9QLUVEHQO vMIoCaBu9sSg4ODrSkbD9CGXtq0TTpq6kq7psLuE
mc mb minio/colorization

mc cp test_image_bw.jpg minio/colorization
http_proxy="" curl -d '{"image": "test_image_bw.jpg"}' http://localhost:8080/function/colorization
mc cp  minio/colorization/1515416868369_output.jpg .

curl http://tsachse720:8080/async-function/colorization -d '{"image": "IMG_1644.jpg"}' -H "X-Callback-Url: https://requestb.in/x4viy4x4"
````
