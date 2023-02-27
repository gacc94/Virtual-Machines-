# CENTOS 7.9 minimal
# Instalacion PHP 7.0.3 

1. Asegúrate de que el sistema esté actualizado usando el siguiente comando:
~~~ 
sudo yum update 
~~~
2. Instala el repositorio EPEL (Extra Packages for Enterprise Linux) usando el siguiente comando:
~~~ 
sudo yum install epel-release
~~~
3. Agrega el repositorio Webtatic usando el siguiente comando:
~~~
sudo rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
~~~
4. Instala PHP 7.0.3 y sus módulos usando el siguiente comando:
~~~ 
sudo yum install php70w php70w-cli php70w-common php70w-devel php70w-mysql php70w-pdo php70w-xml php70w-mbstring php70w-json php70w-zip
~~~
~~~
sudo yum install php70w-cli php70w-common php70w-devel php70w-gd php70w-imap php70w-mbstring php70w-mcrypt php70w-mysql php70w-pdo php70w-pear php70w-xml php70w-xmlrpc
~~~
5. Verificar version PHP
~~~
php -v
~~~

### OTROS COMANDOS
* Verificar modulos de php instalados
~~~
yum list installed php *
~~~

# Instalacion APACHE 2.4.6

1. Instala Apache 2.4.6:
~~~
sudo yum install httpd
~~~

2. Inicia el servicio de Apache:
~~~
sudo systemctl start httpd
~~~

3. Configura Apache para que se inicie automáticamente en el arranque del sistema:
~~~
sudo systemctl enable httpd
~~~

4. Verifica que Apache está en ejecución y escuchando en el puerto 80:
~~~
sudo systemctl status httpd
~~~

5. Abre el puerto 80 y 443 en el firewall:
~~~
sudo firewall-cmd --zone=public --permanent --add-service=http
sudo firewall-cmd --zone=public --permanent --add-service=https
sudo firewall-cmd --reload
~~~
### OTROS COMANDOS
* Revisar estado de apache:
~~~
sudo systemctl status httpd
~~~
* Reiniciar apache para aplicar los cambios hechos:
~~~
sudo systemctl restart httpd
~~~
* Crear archivo de prueba php 
~~~
sudo vi /var/www/html/test.php
~~~
* Ejecuta el siguiente comando para mostrar los puertos en los que está escuchando Apache:
~~~
sudo ss -tulpn | grep httpd
~~~

# Instalacion SSH

1. sudo yum install openssh-server
~~~
sudo yum install openssh-server
~~~
2. Habilitar el servicio de SSH. Para habilitar el servicio de SSH en CentOS 7.9, ejecuta el siguiente comando:
~~~
sudo systemctl enable sshd.service
~~~
3. Iniciar el servicio de SSH. Para iniciar el servicio de SSH, ejecuta el siguiente comando:
~~~
sudo systemctl start sshd.service
~~~
4. (Opcional) Configurar el firewall para permitir el tráfico de SSH. Si el firewall está habilitado en la máquina, puedes configurarlo para permitir el tráfico de SSH con los siguientes comandos
~~~
sudo firewall-cmd --permanent --zone=public --add-service=ssh
sudo firewall-cmd --reload
~~~

### Siguientes pasos para configurar autenticacion con clave publica
1. Genera un par de claves pública-privada en el host desde el que te conectarás a la máquina con el siguiente comando
~~~
ssh-keygen
~~~
2. Copia la clave pública al servidor CentOS 7.9. Para hacerlo, utiliza el siguiente comando en el host:
~~~
ssh-copy-id username@IP_address
~~~

### OTROS COMANDOS
* Revisar la ubicacion del directorio ssh
~~~
echo ~/.ssh
~~~
* Imprimir clave ssh
~~~
cat ~/.ssh/id_rsa.pub
~~~
* Copiar clave ssh a un archivo txt
~~~
cat ~/.ssh/id_rsa.pub > mi_clave_ssh.txt
~~~
* Copiar clave ssh a un archivo txt
~~~
sudo ss -tlnp | grep sshd
~~~
