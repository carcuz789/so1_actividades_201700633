
## Parte 1: Gestión de Usuarios

### 1. Creación de Usuarios
``` bash
sudo useradd usuario1
sudo useradd usuario2
sudo useradd usuario3
```
### 2. Asignación de Contraseñas
``` bash
sudo passwd usuario1
sudo passwd usuario2
sudo passwd usuario3
```

### 3. Información de Usuarios

``` bash
id usuario1
```
### resultado 

### 4. Eliminación de Usuarios

``` bash
sudo userdel -r usuario3

```


## Parte 2: Gestión de Grupos

### 1. Creación de Grupos
``` bash
sudo groupadd grupo1
sudo groupadd grupo2

```

### 2.  Agregar Usuarios a Grupos
``` bash
sudo usermod -aG grupo1 usuario1
sudo usermod -aG grupo2 usuario2


```


### 3. Verificar Membresía
``` bash
groups usuario1
groups usuario2

```
### resultado 

### 4. Eliminar Grupo
``` bash
sudo groupdel grupo2


```

## Parte 3: Gestión de Permisos


### 1. Creación de Archivos y Directorios como usuario1

``` bash
sudo su - usuario1
echo "Contenido de archivo1" > ~/archivo1.txt
mkdir ~/directorio1
echo "Contenido de archivo2" > ~/directorio1/archivo2.txt
exit
```

### 2. Verificar Permisos
``` bash
ls -l ~/archivo1.txt
ls -ld ~/directorio1
```
### resultado 

###  3. Modificar Permisos usando chmod con Modo Numérico

``` bash
chmod 640 ~/archivo1.txt
```