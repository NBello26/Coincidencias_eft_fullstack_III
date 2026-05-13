# 🧩 Microservicio de Coincidencias - Sistema de Gestión de Mascotas

Este repositorio contiene el **Motor de Coincidencias**, un microservicio desarrollado en Spring Boot encargado de la lógica más compleja del sistema: comparar reportes de mascotas perdidas con reportes de mascotas encontradas para generar posibles "matches" basados en características, fechas y datos geográficos.

## 🚀 Arquitectura y Prácticas DevOps

Dada la carga computacional que puede representar el proceso de búsqueda y comparación, este microservicio se ha aislado en una instancia dedicada para garantizar la alta disponibilidad y un rendimiento óptimo de la plataforma.

El flujo de despliegue está totalmente automatizado mediante un pipeline de **CI/CD con GitHub Actions**:
1. Compilación del código fuente y validación de artefactos Java.
2. Construcción de una imagen Docker ligera y segura.
3. Publicación de la imagen en **Amazon Elastic Container Registry (ECR)**.
4. Despliegue automatizado en la instancia **EC2** exclusiva (Nodo Back 4) mediante **AWS Systems Manager (SSM)**.
5. Configuración dinámica de entorno para la comunicación con el Service Registry y la base de datos central.

### 🌐 Ecosistema de Infraestructura en AWS
Este microservicio ocupa el cuarto nodo de backend, operando de forma independiente para maximizar la escalabilidad:

* **Nodo Web:** ApiGateway y Frontend
* **Nodo Back 1:** Eureka Server y BFF
* **Nodo Back 2:** Microservicios de Mascotas y Usuarios
* **Nodo Back 3:** Microservicios de Geolocalización y Notificaciones
* **Nodo Back 4:** **Motor de Coincidencias** (Este repositorio) 📍
* **Base de Datos:** SanosDB (PostgreSQL)

## 🛠️ Tecnologías Principales

* **Framework:** Java 17 / Spring Boot 3
* **Comunicación Interna:** OpenFeign (para consumir datos de Mascotas y Geolocalización)
* **Cloud Native:** Spring Cloud Netflix Eureka Client
* **Contenedores:** Docker
* **CI/CD:** GitHub Actions
* **Infraestructura AWS:** EC2, ECR, SSM, IAM

## ⚙️ Descubrimiento y Lógica Distribuida

* **Orquestación de Datos:** El motor de coincidencias utiliza **OpenFeign** para solicitar dinámicamente información a los microservicios de `Mascotas` y `Geolocalización`.
* **Auto-Registro (Eureka):** Al igual que el resto del ecosistema, se registra en el servidor Eureka bajo el nombre `MS-MOTOR-COINCIDENCIAS`. Esto permite que el BFF pueda invocar los procesos de emparejamiento de forma transparente, sin importar la IP privada que AWS asigne a la instancia del Nodo 4.
* **Consumo de Recursos:** Al estar en una EC2 independiente, el motor puede escalar sus recursos (CPU/RAM) de forma aislada según el volumen de reportes generados en la plataforma.

## 📦 Repositorios del Proyecto

Explora el resto de la infraestructura y microservicios de este ecosistema:

**Frontend y Puertas de Enlace**
* 🌐 [Frontend_eft_fullstack_III](https://github.com/NBello26/Frontend_eft_fullstack_III)
* 🚪 [ApiGateway_eft_fullstack_III](https://github.com/NBello26/ApiGateway_eft_fullstack_III)
* 🌉 [BFF_eft_fullstack_III](https://github.com/NBello26/BFF_eft_fullstack_III)

**Descubrimiento y Base de Datos**
* 🧭 [Eureka_eft_fullstack_III](https://github.com/NBello26/Eureka_eft_fullstack_III)
* 🗄️ [BD_eft_fullstack_III](https://github.com/NBello26/BD_eft_fullstack_III)

**Microservicios de Negocio**
* 🐾 [Reporte_Mascota_eft_fullstack_III](https://github.com/NBello26/Reporte_Mascota_eft_fullstack_III)
* 👤 [Usuarios_eft_fullstack_III](https://github.com/NBello26/Usuarios_eft_fullstack_III)
* 📍 [Geolocalizacion_eft_fullstack_III](https://github.com/NBello26/Geolocalizacion_eft_fullstack_III)
* 🔔 [Notificaciones_eft_fullstack_III](https://github.com/NBello26/Notificaciones_eft_fullstack_III)
* 🧩 [Coincidencias_eft_fullstack_III](https://github.com/NBello26/Coincidencias_eft_fullstack_III) *(Estás aquí)*

---
*Desarrollado como parte del proyecto final de integración de arquitectura DevOps.*
