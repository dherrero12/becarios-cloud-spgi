# Apagar y encender VSI en VPC

Creación de una aplicación contenerizada para automatizar el encendido y apagado de VSI en VPC a través de cron jobs periódicos. 

## Variables de entorno
- VSI_ID: el ID de la máquina virtual en VPC de la cual se desea automatizar el encendido o apagado. 
- STATE: El estado deseado de la máquina, los valores deben ser "on" si se desea encender, "off" si se desea apagar. 
- API_KEY: API_KEY de la cuenta para autenticarse y comprobar que tiene los permisos necesarios para operar con la VSI. 

## Despliegue de la aplicación
1. Crear una imagen Docker a partir del código y Dockerfile disponible. 
2. Almacenar la imagen creada en Container Registry. 
3. Crear un proyecto en Code Engine. 
4. Crear un Job en Code Engine con la imagen, añadiendo como variables de entorno en formato Key-value
```
API_KEY = <your_api_key>
VSI_ID = <VSI_ID>
```
5. Crear un **EVENT SUBSCRIPTION** dentro del proyecto, seleccionando la opción "Periodic Timer" y un nombre. 
6. Añadir como **Event attributes** clave-valor con el estado deseado de la máquina. 
```
STATE = <on or off>
```
7. Seleccionar periocidad del evento. 
8. Crear event subscription. 
9. Repetir los pasos 5-7 con el estado contrario para tener un Event Subscription configurado para apagar y encender la VSI. 
