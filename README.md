# exacq

## edvrserver

Para construir la imagen hay que situarse en el mismo directorio del Dockerfile y ejecutar:

´docker build . --tag exacq-edvrserver:23.09.6.0´

Para arrancar el contenedor de la imagen construida arriba hay que ejecutar:

´docker run -d -p 22609:22609 --network bridge --name exacq-edvrserver exacq-edvrserver:23.09.6.0´

## webservice

Para construir la imagen hay que situarse en el mismo directorio del Dockerfile y ejecutar:

´docker build . --tag exacq-webservice:23.09.6.0 [--build-arg log_level=debug]´

Para arrancar el contenedor de la imagen construida arriba hay que ejecutar:

´docker run -d -p 8080:8181 --network bridge --name exacq-webservice exacq-webservice:23.09.6.0´
