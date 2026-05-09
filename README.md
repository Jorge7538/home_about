# home_about

Un proyecto Django mínimo para una página _Home_ y _About_.

Este repositorio contiene una pequeña aplicación que sirve páginas estáticas usando Django. Está pensado como ejemplo o plantilla para proyectos sencillos y pruebas locales con SQLite.

## ✨ Resumen rápido

- Framework: Django
- Base de datos: SQLite (archivo `db.sqlite3` en la raíz)
- Apps incluidas: `pages` (contiene vistas para `home` y `about`)
- Plantillas: carpeta `templates/` con `_base.html`, `home.html`, `about.html`

## Estructura del proyecto

Raíz del proyecto (destacan los archivos y carpetas principales):

- `manage.py` — utilidades de administración de Django
- `requirements.txt` — dependencias del proyecto
- `db.sqlite3` — base de datos SQLite (creada por Django en local)
- `base_project/` — configuración del proyecto (settings, urls, wsgi, asgi)
- `pages/` — app con vistas, urls y modelos (páginas estáticas)
- `templates/` — plantillas HTML

> Verifica la estructura concreta en la raíz del repositorio si necesitas un mapa visual.

## Requisitos

- Python 3.10+ (se recomienda 3.11)
- pip
- Windows PowerShell (instrucciones específicas a continuación)

Las dependencias están listadas en `requirements.txt`.

## Instalación (PowerShell)

Abre PowerShell en la carpeta del proyecto (por ejemplo: `c:\Users\Jorge Canelon\Pictures\home_about`) y sigue estos pasos:

```powershell
# 1) Crear y activar un entorno virtual
python -m venv .venv
; .\.venv\Scripts\Activate.ps1

# 2) Actualizar pip y luego instalar dependencias
python -m pip install --upgrade pip
; pip install -r requirements.txt
```

Notas sobre PowerShell: si la política de ejecución impide activar el venv, usa:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
; .\.venv\Scripts\Activate.ps1
```

(Esto solo cambia la política para la sesión actual.)

## Preparar la base de datos y ejecutar la app

```powershell
# Asegúrate de estar en el entorno virtual activado
# Aplicar migraciones
python manage.py migrate

# (Opcional) Crear un superusuario para el admin
python manage.py createsuperuser

# Ejecutar servidor de desarrollo en localhost:8000
python manage.py runserver
```

Luego abre http://127.0.0.1:8000/ en tu navegador. Si el proyecto está configurado con rutas, `home` y `about` deberían estar disponibles (por ejemplo `/` y `/about/`).

## Tests

Si hay pruebas en `pages/tests.py` o en otras apps, puedes ejecutar:

```powershell
python manage.py test
```

Esto ejecutará los tests que estén definidos.

## Desarrollo: recomendaciones y buenas prácticas

- Usa un entorno virtual para cada proyecto.
- No subas `db.sqlite3` ni archivos sensibles a repositorios públicos si contienen datos reales.
- Añade un `.gitignore` (si aún no lo tienes) que ignore `.venv/`, `__pycache__/`, `db.sqlite3` y archivos de entorno.

Ejemplo mínimo de `.gitignore`:

```
\.venv/
__pycache__/
db.sqlite3
*.pyc
.env
```

## Despliegue

Este proyecto está preparado para uso local y desarrollo. Para desplegarlo en producción se recomiendan pasos adicionales:

- Cambiar la base de datos a PostgreSQL o similar.
- Configurar `DEBUG = False` en `base_project/settings.py` y definir `ALLOWED_HOSTS`.
- Configurar gestión de secretos (variables de entorno, `django-environ`, etc.).
- Servir archivos estáticos con un servidor (WhiteNoise, CDN, o configurar nginx + collectstatic).
- Usar un servidor WSGI/ASGI (Gunicorn, Daphne, uWSGI) y un proxy inverso en producción.

Si quieres, puedo añadir un ejemplo de configuración para Heroku, Railway o un `Dockerfile`.

## Cómo contribuir

1. Haz un fork del repositorio.
2. Crea una rama descriptiva (p. ej. `feature/nueva-pagina`).
3. Haz tus cambios y añade tests si aplican.
4. Abre un Pull Request apuntando a la rama principal del proyecto.

Usa mensajes de commit claros y atomicidad en los cambios.

## Notas de diseño y plantillas

- La plantilla base está en `templates/_base.html` y las páginas heredan de ella (`home.html`, `about.html`).
- Mantén la lógica de presentación en las plantillas y la lógica de negocio en vistas/servicios.

## Problemas comunes y soluciones rápidas

- "No module named 'django'": activa el entorno virtual y ejecuta `pip install -r requirements.txt`.
- Errores de migraciones: prueba `python manage.py makemigrations` seguido de `python manage.py migrate`.
- Problemas de permisos en PowerShell: usa `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass` temporalmente.

## Licencia

Este repositorio no incluye una licencia explícita por defecto. Si quieres una licencia permissiva, te recomiendo MIT. Aquí hay un ejemplo breve; si quieres que lo añada como `LICENSE`, dímelo.

```
MIT License

Copyright (c) 2026

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction...
```

Puedo añadir un archivo `LICENSE` completo si lo deseas.

---

¿Te gustaría que:

- agregue un `.gitignore` si falta? (puedo crear uno)
- añada un `Dockerfile` o configuración para despliegue?
- incluya instrucciones específicas para pruebas o CI (GitHub Actions)?

Dime cuál prefieres y lo implemento.