Observabilidad
Objetivo
Garantizar la detección temprana de fallos, medir el desempeño de la aplicación y facilitar el análisis de incidentes mediante logs, métricas y alertas.

Logs
Backend
La aplicación Spring Boot debe generar logs estructurados en formato JSON incluyendo:

Timestamp
Nivel de log
Endpoint
Código HTTP
Correlation ID
Mensaje
Ejemplo:

{
  "timestamp":"2026-10-21T13:00:00Z",
  "level":"INFO",
  "correlationId":"abc123",
  "endpoint":"/neo/vehiculos",
  "status":200
}