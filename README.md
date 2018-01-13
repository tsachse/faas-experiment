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
mc config host add minio http://localhost:9000 ZBPIIAOCJRY9QLUVEHQO vMIoCaBu9sSg4ODrSkbD9CGXtq0TTpq6kq7psLuE
mc mb minio/colorization

mc cp test_image_bw.jpg minio/colorization
http_proxy="" curl -d '{"image": "test_image_bw.jpg"}' http://localhost:8080/function/colorization
mc cp  minio/colorization/1515416868369_output.jpg .

curl http://localhost:8080/async-function/colorization -d '{"image": "IMG_1644.jpg"}' -H "X-Callback-Url: https://requestb.in/x4viy4x4"
````

## Kittens vs Tarsiers - an introduction to serverless machine learning

http://jmkhael.io/kittens-vs-tarsiers-an-introduction-to-serverless-machine-learning/

`````
mc policy public minio/colorization
mc policy --recursive links minio/colorization

faas-cli build -f ./tensorflow.yml
faas-cli deploy -f ./tensorflow.yml

curl http://localhost:8080/function/tensorflow -d 'http://localhost:9000/colorization/colorized_test_image_bw.jpg'
tensorflow/test.sh
`````
