# Ambiente de desarrollo para PHP

Este ambiente de desarrollo esta listo para empezar a trabajar, cuenta con base de datos y las principales librerías. Si crees que le hace falta algo por favor aportar. 

## Configuración

Luego de clonar el proyecto  y tener instalado docker solo debe hacer 2 pasos. 

 1. Crear un volumen para que nuestra base de datos no se pierda al reiniciar nuestra imagen.
```bash
sudo docker volume create --name dbdata
```
 2. Construir nuestra imagen si es la primera vez y subir nuestros servicios.
 ```bash
 sudo docker-compose up --build # si es tu primera vez o a realizado un cambio en dockerfile
 sudo docker-compose up # Para el resto de ocaciones.
 ```
 3. Acceder a tu navegador y colocar localhost y podrás ver el archivo phpinfo

**Nota:**  No temas en agregar nuevos archivos php y ver como funcionan en tu ambiente de desarrollo


