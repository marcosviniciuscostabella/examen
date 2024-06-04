Sistema de Gestión de Empleados
En esta práctica, vamos a crear un sistema de gestión de empleados utilizando la programación orientada a objetos en Python.



Crear aplicacion web
Utilizaremos Flask, un popular framework de Python para construir aplicaciones web, para crear una interfaz web para calcular salarios de empleados. 
1.	Crea una ec2, y habre el puerto 5000 en el grupo de seguridad de la ec2

2.	Instalar Flask si aún no lo tienes instalado. Puedes hacerlo ejecutando sudo install Flask  en tu terminal. Si no tienes pip instalado, debes instalarlo en tu servidor con yum o apt segun tu distribucion linux

3.	Crear un archivo llamado app.py y pon el siguiente código:

from flask import Flask, render_template, request
from clases import Empleado, Gerente
 
app = Flask(__name__)
 
# Ruta para el formulario de entrada de datos
@app.route('/')
def formulario():
    return render_template('formulario.html')
 
# Ruta para procesar los datos del formulario
@app.route('/calcular', methods=['POST'])
def calcular():
    nombre = request.form['nombre']
    edad = int(request.form['edad'])
    salario_base = float(request.form['salario_base'])
    tipo_empleado = request.form['tipo_empleado']
 
    if tipo_empleado == 'gerente':
        bono = float(request.form['bono'])
        empleado = Gerente(nombre, edad, salario_base, bono)
    else:
        empleado = Empleado(nombre, edad, salario_base)
 
    salario_mensual = empleado.calcular_salario_mensual()
    return render_template('resultado.html', nombre=nombre, salario=salario_mensual)
 
if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0')
    

4.	Asegúrate de tener los archivos HTML formulario.html y resultado.html en una carpeta llamada templates en el mismo directorio que app.py.

El contenido de formulario.html:
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora de Salario</title>
</head>
<body>
    <h1>Calculadora de Salario</h1>
    <form action="/calcular" method="post">
        <label for="nombre">Nombre:</label><br>
        <input type="text" id="nombre" name="nombre"><br>
        <label for="edad">Edad:</label><br>
        <input type="number" id="edad" name="edad"><br>
        <label for="salario_base">Salario Base:</label><br>
        <input type="number" id="salario_base" name="salario_base"><br>
        <label for="tipo_empleado">Tipo de Empleado:</label><br>
        <select id="tipo_empleado" name="tipo_empleado">
            <option value="empleado">Empleado</option>
            <option value="gerente">Gerente</option>
        </select><br>
        <label for="bono">Bono (solo para gerentes):</label><br>
        <input type="number" id="bono" name="bono" step="any" disabled><br>
        <input type="submit" value="Calcular">
    </form>
    <script>
        document.getElementById('tipo_empleado').addEventListener('change', function() {
            var bonoInput = document.getElementById('bono');
            if (this.value === 'gerente') {
                bonoInput.disabled = false;
            } else {
                bonoInput.disabled = true;
            }
        });
    </script>
</body>
</html>



Y el contenido de resultado.html:
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Resultado</title>
</head>
<body>
    <h1>Resultado</h1>
    <p>El salario de {{ nombre }} es: ${{ salario }}</p>
    <a href="/">Volver al formulario</a>
</body>
</html>


5.	También, necesitarás tener los archivos clases.py que contiene las clases Empleado y Gerente en el mismo directorio que app.py.

Contenido del archivo clases.py
class Empleado:
    def __init__(self, nombre, edad, salario_anual):
        self._nombre = nombre
        self._edad = edad
        self._salario_anual = salario_anual
 
    @property
    def nombre(self):
        return self._nombre
 
    @nombre.setter
    def nombre(self, nuevo_nombre):
        self._nombre = nuevo_nombre
 
    @property
    def edad(self):
        return self._edad
 
    @edad.setter
    def edad(self, nueva_edad):
        self._edad = nueva_edad
 
    @property
    def salario_anual(self):
        return self._salario_anual
 
    @salario_anual.setter
    def salario_anual(self, nuevo_salario):
        self._salario_anual = nuevo_salario
 
    def calcular_salario_mensual(self):
        return self._salario_anual / 12
 
class Gerente(Empleado):
    def __init__(self, nombre, edad, salario_anual, bono):
        super().__init__(nombre, edad, salario_anual)
        self._bono = bono
 
    @property
    def bono(self):
        return self._bono
 
    @bono.setter
    def bono(self, nuevo_bono):
        self._bono = nuevo_bono
 
    def calcular_salario_mensual(self):
        salario_base_mensual = super().calcular_salario_mensual()
        return salario_base_mensual + self._bono / 12
Una vez creados los archivos podemos deplegar nuestra aplicacion con el sigueinte comando:
python3 app.py

Accediendo a la ip de la ec2 en el servidor por el puerto 5000 deberíamos ver nuestro formulario para calcular el salario mensual
Rellena el formulario y calcula el salario, adjunta la captura de pantalla del resultado


