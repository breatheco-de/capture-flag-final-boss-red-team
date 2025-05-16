# FINAL BOSS - El último desafío corporativo

En este laboratorio te enfrentarás a un sitio web aparentemente grande y vulnerable que pertenece a la corporación ficticia **Umbrella Corporation**. A pesar de estar lleno de pistas falsas (SQLi, LFI, etc.), deberás analizar a fondo su estructura, descubrir un archivo de respaldo expuesto y aprovechar una mala configuración en tareas programadas para escalar privilegios en un sistema Windows.

En este laboratorio aprenderás:

- Análisis de sitios web con múltiples señuelos
- Fuzzing de directorios y extracción de credenciales
- Acceso remoto a través de Evil-WinRM
- Escalada de privilegios en Windows usando tareas programadas
- Decodificación de flags cifradas en base64

<how-to-start>
   
## 🌱 Cómo iniciar este laboratorio

Sigue las siguientes instrucciones para comenzar:

1. **Descarga la máquina virtual** desde este [enlace]().
2. **Importa la máquina** en tu gestor de virtualización preferido (VirtualBox, VMware, etc.).
3. Una vez iniciada la máquina, ¡ya puedes comenzar con el laboratorio!
</how-to-start>


## 📄 Instrucciones

Estás frente a un servidor web perteneciente a **Umbrella Corporation**, una empresa con prácticas cuestionables en ciberseguridad. Tu objetivo es acceder al sistema con permisos de administrador y obtener una flag oculta en el escritorio del usuario `Administrator`.

1. **Descubre la dirección IP de la máquina Final Boss.**

2. **Investiga el sitio web.**
   - Accede desde tu navegador a `http://<IP>`.
   - Recorre las rutas como:
     - `index.php?page=home`
     - `index.php?page=about`
     - `index.php?page=contact`

3. **Haz fuzzing para buscar directorios ocultos.** Usa herramientas como `gobuster` o `dirb`

4. **Extrae las credenciales.**

5. **Conéctate a la máquina usando Evil-WinRM.** Usa las credenciales descubiertas para obtener una shell.

6. **Escala privilegios editando un script mal configurado.**

7. **Busca la flag final.** La flag está cifrada en base64. Usa [CyberChef](https://gchq.github.io/CyberChef/) para decodificarla.



**Recuerda:** No todo lo que parece vulnerable lo es. Aprende a seguir las pistas reales entre los engaños.

¡Buena suerte, agente!
