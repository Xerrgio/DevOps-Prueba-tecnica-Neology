Rollback
Objetivo
Restaurar rápidamente una versión estable después de un despliegue defectuoso.

Cuándo ejecutar rollback
Realizar rollback cuando exista alguno de los siguientes síntomas:

Incremento de errores 5xx.
Latencia superior al SLO establecido.
Fallas funcionales críticas.
Incremento anómalo de conexiones a PostgreSQL.
Fallas después de una liberación reciente.
Procedimiento con Docker Compose
1. Identificar la versión estable
Consultar el último tag aprobado:

git tag
2. Cambiar a la versión estable
git checkout <tag-estable>
3. Reconstruir contenedores
docker compose down
docker compose up -d --build
Procedimiento con Kubernetes
Ver historial
kubectl rollout history deployment/backend
Revertir despliegue
kubectl rollout undo deployment/backend
Verificar estado
kubectl rollout status deployment/backend
Validaciones posteriores
Salud de la API
curl http://localhost:8080/actuator/health
Smoke Test
./scripts/smoke-test.sh
Verificación de métricas
Revisar:

Tasa de errores.
Latencia.
Uso de CPU.
Conexiones PostgreSQL.
Comunicación
Informar:

Hora del incidente.
Versión afectada.
Versión restaurada.
Impacto al usuario.
Estado final de recuperación.
Acciones preventivas
Canary deployments.
Validaciones automáticas en CI/CD.
Monitoreo de latencia y errores.
Pruebas de carga antes de producción.
Revisión de cambios de configuración.
Criterios de éxito
El rollback se considera exitoso cuando:

La aplicación responde correctamente.
Los errores regresan a niveles normales.
La latencia vuelve a valores esperados.
Los smoke tests son satisfactorios.
Se restablece el cumplimiento del SLO.