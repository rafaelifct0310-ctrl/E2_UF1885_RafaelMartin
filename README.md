# E2 UF1885 - Detección, análisis y resolución de incidencias (ERP-CRM)

**Alumno:** Martín, Rafael  
**Fecha:** 2026-02-04  
**Entorno:** Ubuntu Server + Docker  
**Contenedores:** odoo-dev (CRM) | postgres-dev (BD)

---

## 1. Análisis inicial del sistema y parámetros de rendimiento
### 1.1 Servicios de acceso al CRM
- Descripción: 
  - Acceso al ERP/CRM (aplicacion web): contendor odoo-dev (Odoo 18)
  - El servicio de base de datos: contenedor postgres-dev (PostgrSQL 16)
  - Servicio de publicación de puerto / acceso web: Docker publica 8069/tcp 
  - Red y DNS del sistema: interfaz la IP 192.168.1.43
  - Acceso administrativo remoto: SSH en 22/tcp para tareas de soporte.
- Evidencias: evidencias/01_analisis/

### 1.2 Parámetros (CPU / RAM / Disco / Red) y relación con CRM+BD

- CPU ~ 95,8% idle, load average: 0,47, 0,43, 0,41
- Conclusiones: No hay saturación de CPU.

- RAM 4,8Gi total;  756Mi usado;  3,3Gi libre
- Conclusiones: Hay suficiente memoria, no hay presión ahora mismo con la RAM. 

- Disco: /dev/sda2   tamaño:25G  usado:12G (52%)
- Conclusiones: No hay problema de capacidad por ahora.

---

## 2. Monitorización de procesos y detección de sobrecarga
### 2.1 Proceso problemático detectado
- Proceso/servicio:
  - Contenedor postgres-dev-PPF (PostgrSQL servicio BBDD ERP/CRM)
  - Proceso interno forzado por el sistema: yes > /dev/null & (generador de carga de CPU)
- Datos y justificación:
  - %CPU : Contenedor Postgres-dev-PPF (1256.16%)
  - Consumo de memoria bajo (164.5MiB/10.69GiB)
  - Saturación se produce a nivel del CPU 
- Impacto en el CRM:
  - Lentitud extrema en operaciones que dependen de la base de datos.
  - Usuarios perciben bloqueos y esperas prolongadas.

---

## 3. Resolución de una incidencia técnica simulada
### 3.1 Síntomas
- Los usuarios no pueden aceder al CRM
- La URL del servicio no responde.
### 3.2 Diagnóstico
- Verificar el estado de los contenedores (docker ps)
- El contenedor odoo-dev-PPF no se encuetra en ejecución
### 3.3 Acción aplicada
- Se procede a restablecer el servicio de contenedor, arrancando nuevamente
  ```
  sudo docker start odoo-dev-PPF
  ```
### 3.4 Verificación
- Verificar estado del contenedor
  ```
  sudo docker ps
  ```
### 3.5 Rollback
- En esta situación consiste en arrancar el contenedor como se indica en la acción aplicada

---

## 4. Simulación de saturación del sistema (CPU o Memoria)
- Técnica utilizada:
  Simulación saturación de memoria RAM mediante ejecución de un proceso que consume gran cantidad de memoria,
  provocando una reducción importante de la memoria libre
- Datos capturados:
  - free -h -> antes y despues de la simulación
  - vmstat 1 5 -> antes y despues de la simulación 
- Análisis:
  - Antes de la simulación el sistema disponia de 4.5Gi de memoria libre. Tras la simulación, la memoria utilizada aumentó a 8.4Gi, el sistema no ha llegado a nivel crítico, pero si un escenario de 
  riesgo.; 
- Verificación requisitos HW/SW:
  El sistema cuenta con 10 GiB RAM y no tiene swap configurada.
  Para entornos ERP/CRM con carga recurrente, esta configuración puede ser insuficiente en picos de
  consumo de memoria.
     Aumentar memoria RAM disponible, o
     configurar swap como medida preventiva
- Registro:
  La simulación se realizó de forma controlada y reversible sin perdida de datos.

---

## 5. Documentación y registro técnico
### 5.1 Incidencias detectadas / Acciones / Resultados
### 5.2 Interpretación de documentación en inglés (monitorización / rendimiento / administración CRM)
- Fragmento 1 (EN): “Docker provides built-in commands to monitor container resource usage, including CPU, memory, and network I/O, which helps identify performance bottlenecks.”
- Interpretación (ES): Docker proporciona comandos integrados que permiten monitorizar el uso de recursos de los contenedores, como CPU y memoria, lo que facilita la identificación de cuellos de botella que pueden afectar al rendimiento del sistema ERP-CRM.
- Fragmento 2 (EN): “High memory usage can significantly impact application performance, potentially leading to slower response times or service instability.”
- Interpretación (ES):
- Fragmento 3 (EN): “Odoo performance issues are often related to system resource constraints, background jobs, or database load, making monitoring and proper sizing essential.”
- Interpretación (ES):
