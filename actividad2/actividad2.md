

# Actividad 2
Guardar el Script en un Archivo
Crear el archivo del script: Abre un editor de texto (como nano, vim, o cualquier otro de tu preferencia) y pega el contenido del script en él. Por ejemplo, usando nano:

````
nano github_user_info.sh
````
###### luego poner el codigo del script


######### Obtener la variable GITHUB_USER
````
GITHUB_USER="$1"
````

######### Validar que la variable GITHUB_USER no esté vacía
````
if [ -z "$GITHUB_USER" ]; then
  echo "Error: Debes proporcionar un nombre de usuario de GitHub."
  exit 1
fi
````

######### Consultar la URL de GitHub API
````
RESPONSE=$(curl -s "https://api.github.com/users/$GITHUB_USER")
````

### Extraer datos del JSON de respuesta
````
USER_ID=$(echo "$RESPONSE" | jq -r '.id')
CREATED_AT=$(echo "$RESPONSE" | jq -r '.created_at')
````

### Validar que los datos hayan sido extraídos correctamente
````
if [ -z "$USER_ID" ] || [ "$USER_ID" == "null" ]; then
  echo "Error: No se pudo obtener el ID del usuario. Verifica que el nombre de usuario de GitHub sea correcto."
  exit 1
fi
````

### Formatear el mensaje
````
MESSAGE="Hola $GITHUB_USER. User ID: $USER_ID. Cuenta fue creada el: $CREATED_AT."
````
### Imprimir el mensaje
````
echo "$MESSAGE"
````

### Crear el directorio para el log basado en la fecha actual
````
DATE=$(date +%Y-%m-%d)
LOG_DIR="/tmp/$DATE"
mkdir -p "$LOG_DIR"
````

### Crear el archivo de log y escribir el mensaje
````
LOG_FILE="$LOG_DIR/saludos.log"
echo "$MESSAGE" >> "$LOG_FILE"
````

## hacer el archivo ejecutable
````
chmod +x github_user_info.sh
````

# Configurar el Cronjob


## Abrir el archivo crontab: Abre el archivo crontab para el usuario actual con el siguiente comando:

````

crontab -e
````

### Añadir el cronjob: Añade la siguiente línea al archivo crontab para ejecutar el script cada 5 minutos. Reemplaza /ruta/al/script/github_user_info.sh con la ruta completa al archivo del script y <GITHUB_USER> con el nombre de usuario de GitHub que deseas consultar.



*/5 * * * * /home/rodrigo/github_user_info.sh carcuz789


### Guardar y salir del editor de crontab: Guarda el archivo crontab y salir del editor para eso se presiona puedes hacer esto presionando Ctrl+O, luego Enter, y Ctrl+X.