Restauración de Base de Datos
Objetivo
Recuperar el servicio ante pérdida de datos, corrupción de la base de datos o recuperación después de un incidente.

Prerrequisitos
Archivo de respaldo disponible.
Credenciales de acceso a PostgreSQL.
Espacio suficiente en disco.
Acceso administrativo al servidor o contenedor.
Procedimiento de restauración
1. Verificar disponibilidad del respaldo
Confirmar que el archivo de respaldo existe y es accesible:

ls -lh parking_backup.sql
2. Detener escrituras en la aplicación
Para evitar inconsistencias se recomienda detener temporalmente el backend:

docker compose stop backend
3. Restaurar la base de datos
psql \
  -U parking \
  -d parking \
  < parking_backup.sql
4. Iniciar nuevamente la aplicación
docker compose start backend
Validación posterior
Verificar:

Salud de la API
curl http://localhost:8080/actuator/health
Resultado esperado:

{"status":"UP"}
Ejecución de smoke test
./scripts/smoke-test.sh
Resultado esperado:

SMOKE TEST CORRECTO
Validación funcional
Acceso correcto al frontend.
Consulta de vehículos.
Consulta de estancias.
Generación del reporte de residentes.
Objetivos de recuperación
RPO (Recovery Point Objective)
15 minutos.

La pérdida máxima aceptable de información es de 15 minutos.

RTO (Recovery Time Objective)
30 minutos.

El servicio debe estar disponible nuevamente en menos de 30 minutos.