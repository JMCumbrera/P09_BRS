# Proyecto 9: Certificados digitales

## Parte 1

En primer lugar instalamos un servidor Ubuntu 23.10, con su servidor OpenSSH y la interfaz de red en modo Adaptador Puente, de modo que nos permita conectarnos al servidor desde nuestro host. 

Ya instalada y preparada la máquina, vamos a nuestro host (Windows 10) y generamos el par de claves pública y privada en la carpeta SSH-Keys (Podríamos generarlas directamente en el directorio *C:\\Users\\{Username}\\.ssh*, pero vamos a copiarlas allí después de transpasar la clave pública al servidor Ubuntu).

![SSH-Keygen](img/ssh-keygen.png)

Como hemos mencionado, debemos copiar nuestra clave pública al servidor Ubuntu, así que para ello hemos decidido abrir un pequeño y momentáneo *servidor http* en el puerto *2345* con *python 3*, para poder descargar la clave directamente desde Ubuntu Server con *wget*. 

![PYTHON3-HTTP-SERVER](img/python3-http-server.png)

![WGET](img/wget.png)

Con la clave pública ya descargada, la movemos al directorio **~/.ssh** del servidor.

![MV_KEY](img/mv-id_rsa.pub.png)

Con esta clave ya en su sitio, copiaremos su contenido al fichero **~/.ssh/authorized_keys**. Antes de hacer esto, nos aseguraremos de asignar los permisos correctos al directorio ssh, cerciorarnos que el fichero authorized_keys existe y asignarle los permisos adecuados.

![authorized_keys](img/cat-ssh-authorized-keys.png)

Como ya tenemos todo configurado, sólo hace falta copiar el par de claves al directorio **C:\\Users\\{Username}\\.ssh**.

![Copy_to_ssh_folder](img/copy-ssh-keys-to-ssh-folder.png)

Finalmente, accedemos vía ssh al servidor Ubuntu Server, y escribimos "*yes*" cuando nos pregunte si queremos continuar conectándonos.

![SSH_Connection](img/ssh-with.keys-active.png)

Como ya podemos autenticarnos a través de nuestra clave pública, deshabilitaremos el acceso por ssh con contraseña, para mayor seguridad. Así evitaremos también ataques por fuerza bruta. Para ello, editaremos el fichero **/etc/ssh/sshd_config**, y cambiaremos a **no** el estado de la variable **PasswordAuthentication**. Luego reiniciaremos el servicio ssh.

![Edit_sshd_config](img/Password_Authentication.png)

![Service_ssh_restart](img/service_ssh_restart.png)

Como podemos ver, con esta configuración nueva, no nos dejará acceder al servidor vía SSH por contraseña.

![SSH_Login_Denied](img/ssh_login_denied.png)
