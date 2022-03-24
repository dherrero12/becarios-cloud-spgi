# Apagar y encender VSI en VPC

Creación de una function para automatizar el encendido y apagado de VSI en VPC a través de cron jobs periódicos. 

## Variables de entorno
- **VSI_ID:** el ID de la máquina virtual en VPC de la cual se desea automatizar el encendido o apagado. 
- **STATE:** El estado deseado de la máquina, los valores deben ser "on" si se desea encender, "off" si se desea apagar. 

## Creación de la función
1. Crear una acción en Functions
2. Asignarle un nombre y seleccionar la versión actual de Python como Runtime. 
3. Copiar y pegar el código disponible en **main.py**. 
4. Dirigirse a **"Connected Triggers"**. 
5. Crear un nuevo trigger de tipo **"Periodic"**.
6. Asignarle un nombre, tiempo y copiar y pegar el siguiente JSON en "JSON Payload". 
```json
{
"VSI_ID": "<VSI_ID>"
"STATE": "<on or off>"
}
```
7. Seleccionar **"Create and connect"**. 
8. Repetir los pasos 5-7 con el estado contrario para automatizar el encendido y apagado de la VSI. 

## API_KEY
Functions inyecta en el codigo una API_KEY como variable de entorno, asociada al namespace de functions donde está creada la accion. El nombre que se le da a dicha variable de entorno es **__OW_IAM_NAMESPACE_API_KEY**.

Para asegurar que la API_KEY tiene los permisos necesarios para apagar/encender VSIs, es necesario seguir los siguientes pasos: 
1. Abre el menu IAM en IBM Cloud. 
2. Selecciona la opción Service IDs de la barra lateral. 
3. Selecciona el Service ID cuyo nombre coincida con el nombre de tu namespace de functions. 
4. Desbloquea el servicio. 
5. Selecciona **Access Policies > Assign access**. 
6. Filtra el recurso de **VPC infrastructure services > Recursos basados en los atributos seleccionados > Resource Type > Virtual Server por VPC**
7. Asigna el siguiente perfil de políticas
- En el área de Platform, selecciona Editor.
- En el área de Resource grouP, selecciona Viewer.
- En el área de Service, selecciona Console Administrator.
8. Bloquea el servicio. 
