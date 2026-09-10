# 🤖 AWS AI Assistant - Cloud Questions Demo

Repositorio para la demostración práctica de un **Asistente de Inteligencia Artificial en AWS** diseñado para responder preguntas sobre la nube. Este proyecto sirve como material educativo para **Bootcamps**, mostrando cómo integrar un Frontend estático, una arquitectura Serverless y Modelos Fundacionales en AWS.

---

##  Tabla de Contenidos
- [Arquitectura de Solución](#arquitectura-de-solución)
- [Estructura del Proyecto](#estructura-del-proyecto)
- [Servicios de AWS Utilizados](#servicios-de-aws-utilizados)
- [Flujo de Información](#flujo-de-información)
- [Prerrequisitos](#prerrequisitos)
- [Paso a Paso: Despliegue en el Bootcamp](#paso-a-paso-despliegue-en-el-bootcamp)
- [Beneficios de esta Arquitectura](#beneficios-de-esta-arquitectura)

---

## Arquitectura de Solución

![Arquitectura del Sistema](./app/Arquitectura.png)

### Componentes de la Arquitectura:
1. **Frontend (Amazon S3):** Hospeda la aplicación web estática (HTML/CSS/JS) mediante S3 Static Website Hosting.
2. **API (Amazon API Gateway):** Expone el endpoint público HTTP `POST /ask` que recibe las preguntas del usuario.
3. **Backend Serverless (AWS Lambda):** Función en Python 3.12 que procesa la petición, construye el prompt con el contexto necesario y consulta al modelo de IA.
4. **Modelo de IA (Amazon Bedrock Runtime):** Servicio administrado que ejecuta el modelo fundacional **Amazon Nova Lite** para generar las respuestas.

---

## no Estructura del Proyecto

```text
.
├── docs/                      # Base de conocimientos / Archivos de texto
│   ├── ec2.txt
│   ├── iam.txt
│   ├── pricing.txt
│   └── s3.txt
├── frontend/                  # Interfaz de usuario (Static Web)
│   ├── app.js                 # Lógica de consumo de la API Gateway
│   ├── index.html             # Estructura del Chat
│   └── style.css              # Estilos visuales de la interfaz
├── lambda/                    # Código de la función Lambda
│   ├── app.py                 # Lógica en Python (Integración con boto3 y Bedrock)
│   ├── lambda.zip             # Paquete compilado de la Lambda
│   └── requirements.txt       # Dependencias Python (boto3)
├── infra/                     # Infraestructura como Código (IaC) con Terraform
│   ├── .gitignore
│   ├── main.tf                # Definición de recursos (S3, API Gateway, Lambda, IAM)
│   ├── outputs.tf             # Outputs (Ej. URL de S3, Endpoint API Gateway)
│   └── provider.tf            # Configuración del proveedor de AWS
├── Arquitectura.png           # Diagrama explicativo de la arquitectura
└── .gitignore
```
##  Servicios de AWS Utilizados
**Amazon S3:** Hosting del sitio web estático.

**Amazon API Gateway:** Gestión y exposición del endpoint REST (POST /ask).

**AWS Lambda (Python 3.12):** Procesamiento sin servidor.

**Amazon Bedrock (Amazon Nova Lite):** Servicio administrado de IA generativa para la respuesta de lenguaje natural.


## Flujo Completo 
**Usuario:** Envía una pregunta desde la interfaz del chat web.

**Frontend:** Realiza una petición POST con la pregunta hacia API Gateway.

**API Gateway:** Invoca la función AWS Lambda.

**Lambda:** Recibe la pregunta, arma el prompt y llama a Amazon Bedrock utilizando el modelo Amazon Nova Lite.

**Bedrock:** Procesa la solicitud y genera una respuesta contextualizada.

**Respuesta:** Bedrock le devuelve la respuesta a Lambda, Lambda a API Gateway, y finalmente la interfaz la muestra en pantalla al estudiante/usuario.
