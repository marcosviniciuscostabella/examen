En esta práctica, vamos a crear un sistema de gestión de empleados utilizando la programación orientada a objetos en Python.


Sistema de distribuición de archivos y directorios
sistema-gestion-empleados/
│
├── app.py                  # Archivo principal de la aplicación Flask
├── clases.py               # Definición de las clases Empleado y Gerente
├── templates/
│   ├── formulario.html     # Formulario HTML para ingresar datos
│   └── resultado.html      # Página HTML para mostrar el resultado
├── requirements.txt        # Lista de dependencias
└── README.md               # Este archivoSistema de Gestión de Empleados


Requisitos tecnicos.

EC2 tamaño t2 small
CLOUD9 tamaño t3


Crear aplicacion web
Crearmos una EC2 en Amazon, nos conectaremos a ella a través de ssh en el Cloud 9.
Nos aseguramos de que tiene python instalado, con python3 --version.

Utilizaremos Flask, un popular framework de Python para construir aplicaciones web, para crear una interfaz web para calcular salarios de empleados. 
El comando para instalar Flask es pip instal Flask

1.	Crea una ec2, y habre el puerto 5000 en el grupo de seguridad de la ec2

2.	Instalar Flask si aún no lo tienes instalado. Puedes hacerlo ejecutando sudo install Flask  en tu terminal. Si no tienes pip instalado, debes instalarlo en tu servidor con yum o apt segun tu distribucion linux

3.	Crear un archivo llamado app.py y pon el siguiente código:

4.	Asegúrate de tener los archivos HTML formulario.html y resultado.html en una carpeta llamada templates en el mismo directorio que app.py.

Este archivo es el index, y muestra el formulario que el cliente tiene que rellenar

Y el contenido de resultado.html:
Muestra el resultado.


5.	También, necesitarás tener los archivos clases.py que contiene las clases Empleado y Gerente en el mismo directorio que app.py.


Una vez creados los archivos podemos deplegar nuestra aplicacion con el sigueinte comando:
python3 app.py

Accediendo a la ip de la ec2 en el servidor por el puerto 5000 deberíamos ver nuestro formulario para calcular el salario mensual



