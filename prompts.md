> Detalla en esta sección los prompts principales utilizados durante la creación del proyecto, que justifiquen el uso de asistentes de código en todas las fases del ciclo de vida del desarrollo. Esperamos un máximo de 3 por sección, principalmente los de creación inicial o  los de corrección o adición de funcionalidades que consideres más relevantes.
Puedes añadir adicionalmente la conversación completa como link o archivo adjunto si así lo consideras


## Índice

1. [Descripción general del producto](#1-descripción-general-del-producto)
2. [Arquitectura del sistema](#2-arquitectura-del-sistema)
3. [Modelo de datos](#3-modelo-de-datos)
4. [Especificación de la API](#4-especificación-de-la-api)
5. [Historias de usuario](#5-historias-de-usuario)
6. [Tickets de trabajo](#6-tickets-de-trabajo)
7. [Pull requests](#7-pull-requests)

---

## 1. Descripción general del producto

**Prompt 1:**  
MailTuner es una herramienta web impulsada por IA que permite **reescribir correos electrónicos en 1 clic**, ajustando su tono comunicativo (formal, claro, empático o persuasivo) sin alterar el contenido original.  

**Prompt 2:**  
Su objetivo principal es mejorar la comunicación profesional y ahorrar tiempo, ofreciendo una interfaz simple donde el usuario pega su correo, elige el tono deseado y obtiene una versión mejorada instantáneamente.  

**Prompt 3:**  
MailTuner sigue un modelo **freemium**, con uso gratuito limitado y planes de suscripción mensual o por créditos. Está orientado a freelancers, equipos de soporte, agencias y profesionales que redactan correos frecuentemente.

---

## 2. Arquitectura del Sistema

**Prompt 1:**  
La arquitectura sigue un enfoque **Serverless + API Gateway** sobre la plataforma **Vercel**, con funciones serverless en Node.js (Next.js API Routes).  

**Prompt 2:**  
El flujo general:  
Frontend (Next.js) → `/api/rewrite` (API interna) → Llamada a **OpenAI API (ChatGPT)** → Respuesta procesada → Renderizado en interfaz.  

**Prompt 3:**  
Servicios complementarios:  
- **Upstash Redis:** rate limiting por IP.  
- **PostHog y Sentry:** analítica y monitoreo de errores.  
- **Google Analytics 4:** seguimiento de tráfico.

### **2.2. Descripción de componentes principales:**

**Prompt 1:**  
**Frontend:** construido con **Next.js + React + TailwindCSS**, gestiona la interfaz y la comunicación con la API.  

**Prompt 2:**  
**API / Backend:** función `/api/rewrite` en **Node.js** que gestiona la comunicación con OpenAI y aplica validaciones de uso y control de peticiones.  

**Prompt 3:**  
**Infraestructura:** desplegada en **Vercel**, con control de peticiones por IP mediante **Upstash Redis REST API** y variables de entorno gestionadas en `.env.local`.

### **2.3. Descripción de alto nivel del proyecto y estructura de ficheros**

**Prompt 1:**  
El proyecto sigue una estructura modular y clara para favorecer el desarrollo colaborativo con asistentes IA (Claude).  

**Prompt 2:**  
Estructura principal:
/mailtuner
│
├── /pages
│ ├── index.tsx # Página principal
│ └── /api/rewrite.ts # Endpoint IA
│
├── /components # Componentes UI reutilizables
│
├── /lib
│ └── rateLimit.ts # Middleware Upstash Redis
│
├── /docs
│ ├── mvp-requirements.md
│ ├── product-specs.md
│ └── technical-specs.md
│
├── .env.local.example
├── package.json
└── README.md

**Prompt 3:**  
El desarrollo está pensado para poder escalar rápidamente, integrando nuevos endpoints de IA y funcionalidades adicionales (p. ej. mejora de textos en LinkedIn o plantillas automáticas).

### **2.4. Infraestructura y despliegue**

**Prompt 1:**  
MailTuner se despliega automáticamente mediante **Vercel**, integrando GitHub como origen de despliegues continuos (CI/CD).  

**Prompt 2:**  
El entorno de producción se configura a través de variables de entorno seguras (`.env.local`) cargadas desde el panel de Vercel.  

**Prompt 3:**  
Infraestructura adicional:
- **Upstash Redis** → rate limit.
- **PostHog & Sentry** → telemetría y errores.
- **GA4** → analítica de tráfico (`G-VXS86QZEKD`).

### **2.5. Seguridad**

**Prompt 1:**  
Se implementa **Rate Limiting por IP** con Upstash Redis REST para evitar abuso de peticiones al endpoint `/api/rewrite`.  

**Prompt 2:**  
Las claves API de OpenAI, Upstash y servicios de analítica se almacenan únicamente en el entorno de Vercel como **variables de entorno**.  

**Prompt 3:**  
El código cumple con principios de **seguridad por defecto**, evitando el almacenamiento de texto sensible y forzando HTTPS en toda la aplicación.

### **2.6. Tests**

**Prompt 1:**

**Prompt 2:**

**Prompt 3:**

---

### 3. Modelo de Datos

**Prompt 1:**  
El sistema es **stateless**, sin base de datos persistente.  

**Prompt 2:**  
Solo se registran métricas anónimas (PostHog) y control de frecuencia (Upstash Redis).  

**Prompt 3:**  
En versiones futuras se planea integrar usuarios con autenticación y almacenamiento de historiales de correos (Firebase o Supabase).

---

### 4. Especificación de la API

**Prompt 1:**  
**Endpoint principal:**  
`POST /api/rewrite`  

**Prompt 2:**  
**Body:**
{
  "text": "Texto original del correo",
  "tone": "formal | claro | empático | persuasivo"
}

---

### 5. Historias de Usuario

**Prompt 1:**  
Como usuario, quiero pegar un correo y elegir un tono para obtener una versión mejorada del texto.  

**Prompt 2:**  
Como usuario gratuito, quiero saber cuántos usos me quedan para decidir si me suscribo.  

---

### 6. Tickets de Trabajo

**Prompt 1:**  
- Implementar endpoint `/api/rewrite` y conexión con OpenAI.  
- Añadir middleware de rate limiting con Upstash Redis.  
- Crear UI inicial con selector de tono y campo de texto.  

**Prompt 2:**  
- Integrar PostHog y Sentry.  
- Configurar despliegue automático en Vercel.  
- Redactar documentación de entorno (`technical-specs.md`).  

**Prompt 3:**  
- Añadir test unitarios para componentes UI.  
- Optimizar rendimiento del renderizado.  
- Preparar landing page de lanzamiento.  

---

### 7. Pull Requests

**Prompt 1:**  
Añadido endpoint `/api/rewrite` y configuración de entorno.  

**Prompt 2:**  
Creación de interfaz inicial con TailwindCSS y selector de tono.  

**Prompt 3:**  
Integración de Upstash Redis, PostHog y Sentry + documentación completa.  
