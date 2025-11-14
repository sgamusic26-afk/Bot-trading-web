# Trading Bot Web - Starter

Este repositorio contiene una **app web mínima** (Flask) que permite:
- Registrar usuarios
- Definir un propietario único (OWNER_EMAIL env var)
- El propietario puede autorizar usuarios a usar el bot
- Ejecutar un bot simulado periódicamente (scheduler)
- Iniciar/detener el bot desde el panel (simulado)

## Características clave
- Propietario único: define la variable de entorno `OWNER_EMAIL` antes de crear cuentas; el usuario con ese correo será marcado como owner al registrarse.
- Multiusuario: el owner puede permitir que otros usuarios usen el bot (toggle desde panel).
- Acceso desde celular: la app es responsive y funciona desde Safari en iPhone.

## Archivos principales
- `app.py` - código principal (Flask)
- `templates/` - vistas (Bootstrap)
- `static/` - archivos estáticos
- `requirements.txt` - dependencias

## Cómo ejecutar (local / VPS)
1. Clonar el repo o subir los archivos al servidor.
2. Crear virtualenv e instalar:
   ```bash
   python -m venv venv
   source venv/bin/activate
   pip install -r requirements.txt
   ```
3. Opcional: exportar variables de entorno
   ```bash
   export OWNER_EMAIL="tuemail@dominio.com"
   export FLASK_SECRET="cambiame_por_una_clave_segura"
   ```
4. Inicializar base (se crea automáticamente SQLite) y ejecutar:
   ```bash
   python app.py
   ```
5. Abrir en el navegador del iPhone: `http://<tu-ip>:5000/`
   - Para acceso seguro desde internet: desplegar en VPS con HTTPS (nginx) o usar servicios como Render/Heroku/Vercel (con Gunicorn) o exponer localmente con `ngrok`.

## Pasos recomendados antes de usar en real
- Añadir HTTPS (nginx + Let's Encrypt)
- Implementar límites de tasa y protección CSRF
- Revisar y asegurar `SECRET_KEY`
- Implementar manejo de claves API de brokers en un vault o variables locales, NO en la DB sin cifrado
- Añadir comisiones, slippage y órdenes limitadas si vas a operar real

## Convertir a Docker (opcional)
Ejemplo Dockerfile:
```dockerfile
FROM python:3.11-slim
WORKDIR /app
COPY . /app
RUN pip install -r requirements.txt
ENV FLASK_ENV=production
CMD ["python","app.py"]
```

## Nota legal
Esto es un **starter kit** educativo. No uses con capital real sin auditar y probar en paper trading.