# Respuestas — Laboratorio de Observabilidad
## 1. ¿Por qué necesitamos Loki además de Prometheus si ya tenemos /metrics?
Prometheus es útil para ver métricas numéricas como el uso de CPU o la cantidad de peticiones, pero no te muestra qué pasó internamente en la aplicación. Loki complementa esto guardando los logs de texto, como cuando en el lab filtramos por level="ERROR" y vimos exactamente qué errores estaba generando el backend. Sin Loki, solo sabrías que algo falló, pero no por qué.

## 2. ¿Qué ventaja aporta que las fuentes de datos de Grafana estén aprovisionadas como código y no creadas a mano?
Al levantar el stack con docker compose up, Grafana ya tenía Prometheus y Loki configurados automáticamente gracias al archivo datasources.yml. Si eso no existiera, cada vez que reiniciara el entorno tendría que entrar a Grafana y configurarlos a mano. Con el archivo, cualquier persona puede reproducir el mismo entorno sin pasos adicionales.

## 3. El panel "CPU contenedor" y el panel "CPU host" pueden mostrar valores muy distintos. ¿Por qué? ¿Cuál usarías para alertar sobre una aplicación concreta?
El panel del host muestra el consumo de toda la máquina, incluyendo procesos del sistema operativo y otros servicios. El panel del contenedor mide solo el proceso específico del backend. Para alertar sobre una aplicación concreta usaría el del contenedor, porque es más preciso y no se ve afectado por otros procesos ajenos a la app.

## 4. ¿Qué diferencia hay entre el evaluation interval y el pending period de una alarma?
El evaluation interval define cada cuánto Grafana evalúa la métrica, en el lab fue cada 10 segundos. El pending period es el tiempo que la condición debe mantenerse activa antes de disparar la alarma, configuramos 30 segundos. Esto lo comprobamos cuando la alarma llegó a Pending pero volvió a Normal porque la métrica no se sostuvo los 30 segundos necesarios.