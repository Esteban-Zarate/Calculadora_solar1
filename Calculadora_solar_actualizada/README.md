# Energía Viva Solar — versión integrada

Esta versión conserva la identidad visual y la interfaz de Calculadora Solar (carpeta 1) e integra las mejoras funcionales de `paneles_solares` (carpeta 2), incluido el módulo de sitio y montaje.

## Ejecutar

```bash
pip install -r requirements.txt
streamlit run solar_app.py --server.port 8501
```

La aplicación utiliza SQLite local por defecto y conserva la base de datos de la carpeta 1. Si se configuran `TURSO_DATABASE_URL` y `TURSO_AUTH_TOKEN`, los módulos compatibles pueden utilizar Turso.

No publiques `solar_calc.db`, `.streamlit/secrets.toml` ni claves API. Configura SMTP/IA solo mediante secretos o variables de entorno.
