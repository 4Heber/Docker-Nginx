<img src="https://user-images.githubusercontent.com/77643882/168807788-6baf57fe-e6fc-4226-8536-dcf58910fe5c.png" alt="docker-logo" width="100" heigth="100" />

# Docker-Nginx

Desplegar HTML personalizado en server web dockerizado Nginx

## Instalar imagen Nginx

Si contamos con Docker desktop, en el apartado de 'home' encontramos una serie de recomendaciones, entre ellas *Nginx* podemos hacer click en 'run' o ejecutar el siguiente comando por consola:

![01-nginxImage](https://user-images.githubusercontent.com/77643882/168804870-d4884199-8f65-4a44-8736-2bceb2a028c2.png)

```
docker run --rm -d -p 8080:80 --name web nginx
```

![02-downloadNginxImage](https://user-images.githubusercontent.com/77643882/168805030-161e8b40-ec0c-4fe6-a279-fdbc5baa48c0.png)

Para comprobar la correcta instalación, navegamos al puerto definido en el comando *http://localhost:8080* .

![03-wellcomeMSG](https://user-images.githubusercontent.com/77643882/168805063-a05e1f94-f388-44c3-b4e7-0c077f685f4d.png)

Podemos ver el mensaje de bienvenida por defecto con el que cuenta Nginx en su fichero html.

Detenemos el contenedor mediante:

```
docker stop web
```

## Agregar HTML creando imagen personalizada

Para crear una imagen personalizada crearemos un archivo `Dockerfile` y le agregaremos nuestros comandos.

![dockerfile](https://user-images.githubusercontent.com/77643882/168807212-a803159e-49ec-4970-862c-028e2a562c99.png)

```Dockerfile
FROM nginx:latest
COPY ./site-content/index.html /usr/share/nginx/html/index.html
```

Se construye una imagen personalizada usando una imagen base.

El comando `FROM` extraerá la última imagen de `nginx` a nuestra máquina local y luego construirá nuestra imagen personalizada encima de ella.

A continuación, copiamos nuestro archivo `index.html` en el directorio /usr/share/nginx/html dentro del contenedor, sobrescribiendo el archivo `index.html `predeterminado proporcionado por nginx.

Construiremos la imagen con el siguiente comando:

```
docker build -t webserver .
```

El comando de compilación le dirá a Docker que ejecute los comandos ubicados en nuestro Dockerfile.

![06-buildImageFromDockerFile](https://user-images.githubusercontent.com/77643882/168806936-301afcd6-4a63-4c36-9dde-ae5e6433546c.png)

Ahora podemos ejecutar nuestra imagen en un contenedor, pero esta vez no tenemos que crear un volumen para incluir nuestro html pues ya lo hacemos en el Dockerfile al copiar el archivo.


![07-output](https://user-images.githubusercontent.com/77643882/168807641-cc9da4cb-4123-4082-935b-a44285d80dd9.png)









