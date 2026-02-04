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
- Datos y justificación:
- Impacto en el CRM:

---

## 3. Resolución de una incidencia técnica simulada
### 3.1 Síntomas
### 3.2 Diagnóstico
### 3.3 Acción aplicada
### 3.4 Verificación
### 3.5 Rollback

---

## 4. Simulación de saturación del sistema (CPU o Memoria)
- Técnica utilizada:
- Datos capturados:
- Análisis:
- Verificación requisitos HW/SW:
- Registro:

---

## 5. Documentación y registro técnico
### 5.1 Incidencias detectadas / Acciones / Resultados
### 5.2 Interpretación de documentación en inglés (monitorización / rendimiento / administración CRM)
- Fragmento 1 (EN):
- Interpretación (ES):
- Fragmento 2 (EN):
- Interpretación (ES):
- Fragmento 3 (EN):
- Interpretación (ES):
