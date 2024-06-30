<p align="center"><img src="https://github.com/ccalvop/PY-EmailSender/assets/126183973/dbf8c6a6-abde-40bb-a162-5c52cc8f04ce" /></p>

Este proyecto proporciona un script en Python para enviar correos electrónicos utilizando el servidor SMTP de Gmail. Incluye una función para configurar los detalles del correo electrónico y enviar mensajes de manera segura.

**Objetivo**

El objetivo de este proyecto es permitir a los usuarios enviar correos electrónicos de forma programática utilizando un script en Python, sin exponer la contraseña real de su cuenta de Gmail. En su lugar, se generará una contraseña de aplicación para una mayor seguridad.

**Software o Servicios Utilizados**

- Python
- Cuenta de Gmail con verificación en dos pasos habilitada

**Instrucciones**

Para utilizar este script, sigue estos pasos:

1. Habilita la verificación en dos pasos para tu cuenta de Google.  
2. Crea una [contraseña de aplicación](https://support.google.com/accounts/answer/185833?hl=en) en tu cuenta de Google.  
3. Copia y pega la contraseña de la aplicación en el script en el lugar designado.  

**Código Python**

**El script** incluye una función enviar_correo que configura los detalles del correo electrónico y envía el correo de manera segura a través del servidor SMTP de Gmail. Para utilizarlo, simplemente llama a la función con la dirección de correo del destinatario, el asunto y el mensaje.  
La función la he llamado `enviar_correo` con parámetros: `destinatario`, `asunto` y `mensaje`. Se utiliza una contraseña de aplicación para autenticarse en Gmail y enviar el correo.

```python
def enviar_correo(destinatario, asunto, mensaje):
    # Configurar los detalles del correo electrónico
    remitente = 'sender@gmail.com'
    app_password = "google app password (not account password)" # 16-digit app password
    servidor_smtp = 'smtp.gmail.com'
    puerto_smtp = 465  # Utilizamos el puerto 465 para SSL
    
    # Crear el objeto mensaje
    msg = EmailMessage()
    msg.set_content(mensaje)
    msg['Subject'] = asunto
    msg['From'] = remitente
    msg['To'] = destinatario

    # Iniciar la conexión y enviar el correo
    context = ssl.create_default_context()
    try:
        with smtplib.SMTP_SSL(servidor_smtp, puerto_smtp, context=context) as server:
            server.login(remitente, app_password)
            server.send_message(msg, from_addr=remitente, to_addrs=destinatario)
        print("Correo electrónico enviado correctamente.")
    except Exception as e:
        print(f"Error al enviar el correo electrónico: {e}")
```

**Implementación:**

```python
# Construir el mensaje para el correo electrónico
mensaje = f"""
Este es un mensaje de ejemplo que envía variables del programa ejecutado:
variable retornada1 {variable1}
variable retornada2: {variable2}
variable retornada3: {variable3}
"""
# Enviar correo electrónico con el mensaje
destinatario = 'destinatario@gmail.com'
asunto = 'asunto'
enviar_correo(destinatario, asunto, mensaje)
```

**Resultado**

Al ejecutar el script, se enviará un correo electrónico al destinatario especificado con el asunto y el mensaje proporcionados.  
(*)Ten precaución con la contraseña de aplicación generada, ya que proporciona acceso a tu cuenta de Gmail para enviar correos electrónicos.

![diagram](https://github.com/ccalvop/PY-EmailSender/assets/126183973/0c975b6a-7607-422c-934a-25a4acf22a5b)

TIME - 2024-06-30 19:52:28