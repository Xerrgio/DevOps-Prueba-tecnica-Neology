Seguridad
Objetivo
Garantizar que la aplicación pueda ejecutarse de forma segura, evitando la exposición de secretos, reduciendo la superficie de ataque y detectando vulnerabilidades de manera temprana durante el ciclo de vida del software.

Controles implementados
Gestión de secretos
Se eliminó el uso de credenciales embebidas dentro de los archivos de configuración.

Las credenciales se externalizaron mediante variables de entorno:

POSTGRES_DB
POSTGRES_USER
POSTGRES_PASSWORD
Se agregó un archivo .env.example para documentar las variables requeridas sin exponer valores reales.

El archivo .env debe incluirse en .gitignore y nunca debe almacenarse en el repositorio.

Propuesta para producción
Los secretos deben almacenarse en:

GitHub Secrets
Azure Key Vault