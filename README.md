nfs_setup.yml

 Este es un playbook orientado a la instalacion y puesta en marcha de un storage basado en la red, mediante el servicio NFS (Network File System) en entornos
Linux basados en distribuciones CentOS.

Tareas: - Instala el servicio NFS.

	- Se asegura de que el daemon este en ejecucion.

	- Permite las conexiones en el firewall a traves del puerto 2049.

	- Crea o se asegura de que exista el directorio /var/nfs_shared perteneciente al usuario/grupo /nobody/nobody con los permisos 777

	- Garantiza que el directorio esta siendo compartido por NFS.

	- Acualiza el archivo /etc/export en el caso de que este cambie.

uso: ansible-playbook nfs_setup.yml

variables: - Directorio: Ubicacion donde se desea crear el directorio a compartir. Ej: /var/nfs_shared

	   - Opciones: Parametros para el funcionamiento del servicio ubicados en el archivo /etc/export

	   - Permisos: Privilegios que se le otorgaran al usuario especificado sobre el directorio creado.


hardening.yml

 Este playbook ejecuta una serie de tareas especificas enfocadas en fortalecer la seguridad de las conexiones SSH de los equipos sobre los que se ejecute.
Esta pensado para actuar sobre distribuciones Ubuntu.

Tareas: - Actualiza todos los paquetes.

	- Configura Ubuntu Firewall de modo que este bloquee todo el trafico entrante unicamente permitiendo el relacionado a SSH.

	- Gestiona que unicamente se pueda iniciar sesion mediante el uso de una clave publica  (id_<algoritmo>.pub) y hace que el usuario root no pueda
	 hacer login.

	- Instala o Verifica que este instalada la erramienta Fail2Ban y la configura para que bloquee intentos fallidos de conexion definiendo un rango de
	 3 intentos como maximo antes de bloquear la conexion por completo durante un cierto periodo de tiempo establecido. Tambien se asegura que el servicio
	 este funcionando.

	- En el caso de que ocurra una actualizacion de paquetes, el playbook lleva a cabo un reinicio del sistema.

	- Si cambia la configuracion de SSH, este servicio es reiniciado.


uso: ansible-playbook hardening.yml

variables: - Directorio: Ubicacion donde se encuentra el archivo de configuracion de Fail2Ban.
	
	   - Permisos: Privilegios con los que contara el archivo de configuracion de Fail2Ban.
