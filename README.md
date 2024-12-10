# Implementación de Canary Deployments en UpCommerce: Un Enfoque para Mitigar Riesgos

## Contexto

Como nuevo líder del equipo SRE en UpCommerce, has recibido un informe crítico: **UpCommerce.com**, una plataforma de comercio electrónico que atiende a más de 10,000 comerciantes en Norteamérica, está enfrentando problemas de latencia y estabilidad durante horarios pico. En el último trimestre:

- Las quejas por la lentitud del sitio han aumentado un **40%**.
- Hubo **tres caídas importantes** durante el Black Friday del año pasado.
- Los **rollbacks** de despliegues problemáticos tomaron en promedio **45 minutos**, ocasionando pérdidas significativas de ingresos.

El equipo SRE propone implementar una estrategia de **canary deployments** para mitigar estos riesgos y probar nuevas versiones de manera segura. La estrategia permitirá enrutar un **20% del tráfico** a la nueva versión de la aplicación mientras el resto permanece estable. Esto incluye:

- Configurar monitoreo y alertas para detectar problemas rápidamente.
- Definir métricas de éxito y activadores automáticos de rollback.
- Usar **Helm** para gestionar los despliegues.

El objetivo del proyecto es demostrar un concepto probado en **dos semanas**, implementando esta estrategia en una versión simplificada del front-end de UpCommerce.

---

## Objetivo del Proyecto

Este proyecto te guiará para implementar **canary deployments**, configurar monitoreo y automatizar despliegues seguros. Aprenderás a usar herramientas modernas de DevOps para resolver desafíos reales en un entorno de comercio electrónico de alta exigencia.

---

## Pasos Iniciales

### 1. Preparar el Entorno
- Usa **GitHub Codespaces** con una máquina de 4 núcleos y 16 GB de RAM.
- Clona y abre un Codespace en tu fork del repositorio de este proyecto.

### 2. Configurar Minikube
- Inicia un clúster de Kubernetes con:
  ```
  minikube start

- Habilita el complemento de Ingress
  ```
  minikube addons enable ingress

- Crea un namespace para el proyecto:
  ```
  kubectl create namespace canary-demo 

### 3. Estructura del Proyecto
- Aplicación de UpCommerce: Una app Flask que muestra una página HTML con diferentes colores de fondo:
  - Blanco: Versión estable (v1).
  - Verde: Versión canary (v2).
- Configuración Docker: Imágenes preconstruidas disponibles en Docker Hub:
  - uonyeka/canary-demo:v1
  - uonyeka/canary-demo:v2
- Helm Charts: Plantillas para manejar ambos despliegues (estable y canary), configurar servicios, y habilitar monitoreo con Prometheus.

### 4. Tareas Requeridas
- 1. Implementar Despliegues
  Configura despliegues para las versiones estable y canary en un clúster Minikube.
  Asegúrate de enrutar el tráfico en una proporción 80:20.
- 2. Configurar Monitoreo
  Usa Prometheus y Grafana para monitorear los despliegues.
- 3. Actualizar y Desplegar
  Implementa una nueva versión canary (v3) disponible en Docker Hub:
  ```
  uonyeka/canary-demo:v3

### 5. Realizar Rollback
Ante comentarios de los usuarios, regresa a la versión previa de canary (v2).

### 6. Completar answers.yml

### Estructura del Helm Chart
deployment.yaml: Configura los despliegues de ambas versiones.
ingress.yaml: Define reglas de enrutamiento para el tráfico.
servicemonitor.yaml: Habilita monitoreo con Prometheus.
values.yaml: Centraliza configuraciones como versiones de imagen, réplicas y ajustes de canary.
Testing
El proyecto incluye pruebas unitarias en ./tests/test_app.py para validar:

### Respuestas correctas de ambas versiones (colores de fondo).
Exposición de métricas en /metrics.
Distribución de tráfico esperada (80:20).

