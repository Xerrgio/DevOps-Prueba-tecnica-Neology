Respaldo de Base de Datos
Objetivo
Garantizar la recuperación de información ante fallos operativos, errores humanos o corrupción de datos.

Estrategia
Se propone realizar respaldos automáticos diarios de PostgreSQL y conservarlos por al menos 7 días.

Respaldo manual
pg_dump \
  -U parking \
  -d parking \
  > parking_backup.sql