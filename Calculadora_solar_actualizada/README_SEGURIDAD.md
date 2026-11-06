# Seguridad de Calculadora Solar

## Qué cambió

- Las contraseñas nuevas se almacenan con **bcrypt** (`bcrypt.gensalt(rounds=12)`).
- Las contraseñas antiguas SHA-256 se aceptan solo durante la migración y se convierten automáticamente a bcrypt después de un inicio de sesión correcto.
- El registro público siempre crea usuarios con rol `visualizador`.
- El rol de una cuenta no puede ser enviado por el formulario público.
- El cambio de rol sigue reservado al Super Administrador.
- El cambio/restablecimiento de contraseña utiliza bcrypt.
- El cambio de contraseña del propio usuario verifica primero su contraseña actual.
- Se mantienen auditoría, activación/desactivación y sesión temporal del Super Administrador.
- Las consultas de SQLite utilizan parámetros `?` y no concatenan contraseñas ni nombres de usuario directamente.
- Las credenciales iniciales ya no están escritas en el código fuente.

## Configuración local

1. Copia `.env.example` a `.env`.
2. Cambia `ADMIN_PASSWORD` por una contraseña fuerte.
3. No publiques `.env` ni `.streamlit/secrets.toml`.
4. Instala dependencias:

```bash
pip install -r requirements.txt
```

5. Ejecuta la aplicación con el mismo comando que utilizabas para Calculadora Solar.

### Instalación nueva

Si no existe `solar_calc.db`, la aplicación crea el Super Administrador `admin` usando `ADMIN_PASSWORD`.

Si quieres crear también a Jabes en una instalación completamente nueva, configura `JABES_PASSWORD` antes de iniciar la aplicación.

### Instalación existente

La base incluida en este proyecto puede contener hashes SHA-256 de una versión anterior. **No es necesario conocer ni editar esos hashes.** Cuando cada usuario inicie sesión correctamente, el sistema verifica el hash antiguo y lo reemplaza inmediatamente por un hash bcrypt.

Después de cambiar una contraseña desde el perfil o desde Gestión de Usuarios, esa cuenta ya queda con bcrypt.

## GitHub

El archivo `.gitignore` bloquea:

- `.env`
- `.streamlit/secrets.toml`
- bases de datos SQLite
- archivos temporales y cachés de Python

Nunca guardes contraseñas reales en `README.md`, JavaScript, HTML, archivos `.py` o commits de Git.

## Producción

- Usa HTTPS.
- No ejecutes Streamlit en modo debug.
- Usa una contraseña única y larga para el Super Administrador.
- Mantén `bcrypt` actualizado dentro del rango probado por el proyecto.
- Haz copias de seguridad de la base de datos de forma privada.
- No compartas el archivo `solar_calc.db` si contiene datos reales de usuarios.
