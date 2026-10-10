# Proyecto-23-Chatbot-Asistente-en-la-Nube-para-Atencion-Automatizada
Chatbot asistente en la nube con Dialogflow CX e integracion a WhatsApp y Google Sheets para Centro de Servicios Digitales Cuidadanos CSDC

markdown
# 🤖 Chatbot Asistente en la Nube - CSDC (Versión Lite)

Este repositorio contiene la documentación, flujos y scripts de integración para el chatbot automatizado del *Centro de Servicios Digitales Ciudadanos (CSDC). El sistema está diseñado para reducir los tiempos de respuesta y mitigar la sobrecarga de atención manual mediante el uso de **Dialogflow CX, **WhatsApp* y *Google Sheets*.

## 🚀 Características del Asistente
* *Preguntas Frecuentes (FAQ):* Respuestas automatizadas sobre horarios de atención e información general.
* *Consulta de Estados:* Flujo interactivo y guiado sobre las etapas de trámites y expedientes.
* *Registro de Solicitudes:* Formulario interactivo que recopila datos en caliente y los almacena externamente.
* *Omnicanalidad:* Integración directa con el canal de WhatsApp mediante Twilio.

## 🛠️ Arquitectura del Sistema
csdc-chatbot-dialogflow/
│
├── 📄 README.md               <-- Documentación arquitectónica, guía de despliegue y flujos
├── 📁 dialogflow-agent/
│   └── 📄 agent-export.json   <-- Flujo completo (Pages de Menú de Estados y Formularios)
└── 📁 webhook/
    └── 📄 sheets-connector.js <-- Código de Google Apps Script optimizado para el registro de datos

Canal Digital: WhatsApp / Web]
               │
               ▼
┌──────────────────────────────┐
│  LÍNEA 1: Dialogflow CX      │ ➔ (Resuelve 80% de FAQ: Horarios, Requisitos, Estados)
└──────────────┬───────────────┘
               │ (Requiere trámite complejo o soporte)
               ▼
┌──────────────────────────────┐
│  LÍNEA 2: Equipo CSDC        │ ➔ (Atiende casos de alto valor desde una base de datos)


## 🛠️ Arquitectura del Sistema
Usa el código con precaución.
[Ciudadano en WhatsApp] ➔ [Twilio API] ➔ [Dialogflow CX] ➔ [Apps Script] ➔ [Google Sheets]

## 📋 Requisitos Previos
Antes de desplegar el asistente, asegúrate de contar con:
1. Una cuenta activa en *Google Cloud Platform (GCP)* con Dialogflow CX habilitado.
2. Un número de prueba o comercial en *Twilio* (con el Sandbox de WhatsApp configurado).
3. Una hoja de cálculo en *Google Sheets* con acceso de edición para Apps Script.

## ⚙️ Instrucciones de Despliegue

### 1. Dialogflow CX
* Importa el agente en tu consola utilizando el archivo JSON del flujo (si aplica).
* Configura las intenciones clave: csdc.consultar_horarios, csdc.requisitos_tramites, csdc.estado_solicitud y csdc.crear_solicitud.

### 2. Conector de Google Sheets (Apps Script)
1. Abre tu Google Sheets y dirígete a Extensiones > Apps Script.
2. Pega el código que se encuentra en la carpeta /webhook/code.js de este repositorio.
3. Implementa como *Aplicación Web, configura el acceso para *Cualquiera y copia la URL generada.
4. Vincula la URL en el apartado de *Webhooks* dentro de Dialogflow CX.

### 3. Integración con WhatsApp (Twilio)
* Ve a Manage > Integrations en Dialogflow y activa Twilio.
* Copia la Webhook URL provista por Dialogflow y pégala en la configuración del Sandbox de WhatsApp en Twilio (When a message comes in).

## 📁 Estructura del Repositorio
* /dialogflow-agent/: Respaldos y exportaciones del flujo conversacional.
* /webhook/: Código fuente de Google Apps Script para la persistencia de datos.
* README.md: Documentación principal del sistema (este archivo).

## 📄 Licencia
Este proyecto es propiedad del *Centro de Servicios Digitales Ciudadanos (CSDC)*. Todos los derechos reservados.


markdown
## 🛠️ Manual de Mantenimiento Operativo (Para Personal del CSDC)

Para mantener el chatbot actualizado frente a nuevos trámites, convocatorias o cambios institucionales, siga estos pasos:

### 1. ¿Cómo agregar o modificar una Pregunta Frecuente (FAQ)?
Si la institución cambia un horario o añade un requisito, no requiere modificar código:
1. Ingrese a la consola de *Dialogflow CX* y seleccione el agente Asistente-Lite.
2. Vaya a *Manage > Intents* en el menú izquierdo.
3. Seleccione la intención que desea actualizar (ej. csdc.consultar_horarios o csdc.requisitos_tramites).
4. Si los ciudadanos usan nuevas palabras para preguntar lo mismo, agréguelas en *Training Phrases*.
5. Vaya a la pestaña *Build, haga clic en la página donde se da la respuesta, localice la ruta asociada y actualice el texto dentro de **Agent responses*.
6. Haga clic en *Save*.

### 2. Gestión de Respuestas No Entendidas (No-Match)
Una vez a la semana, el supervisor del CSDC debe revisar qué preguntas no pudo responder el bot:
1. En Dialogflow CX, vaya a *Manage > Analytics* o revise la sección *Manage > Intent Training*.
2. Identifique las frases alojadas en el grupo de eventos sys.no-match-default (preguntas que el bot ignoró).
3. Asigne esas frases a las intenciones correctas existentes o cree una nueva intención si es un trámite nuevo que la ciudadanía está empezando a demandar.


markdown
# 🤖 Chatbot Asistente en la Nube - CSDC (Producción)

Este repositorio contiene la arquitectura completa, flujos y scripts de integración del asistente virtual del *Centro de Servicios Digitales al Ciudadano (CSDC)*. La solución mitiga el trabajo manual absorbiendo preguntas frecuentes por WhatsApp y estructurando casos complejos en la nube.

## 📋 Arquitectura del Ecosistema
Usa el código con precaución.
[Ciudadano en WhatsApp] ➔ [Twilio API] ➔ [Dialogflow CX] ➔ [Apps Script] ➔ [Google Sheets]

## 📁 Contenido del Repositorio
* /dialogflow-agent/: Contiene el archivo estructurado JSON para importar el árbol de decisiones del bot en la consola de Google.
* /webhook/: Contiene el código Javascript de producción para Google Apps Script que conecta las interacciones con la base de datos.

## 🛠️ Configuración de la Base de Datos e Indicadores SLA
Para garantizar el correcto funcionamiento del script y el semáforo visual de control de gestión, la hoja de cálculo de *Google Sheets* debe configurarse exactamente con las siguientes columnas en la primera fila (Fila 1):

1. *A1:* Fecha Solicitud (Ingresado por Webhook)
2. *B1:* Nombre Ciudadano (Ingresado por Webhook)
3. *C1:* Correo Electrónico (Ingresado por Webhook)
4. *D1:* Detalle Solicitud (Ingresado por Webhook)
5. *E1:* Acepta Privacidad (Ingresado por Webhook)
6. *F1:* Fecha Respuesta (Ingresado manualmente por el funcionario en formato dd/mm/aaaa hh:mm:ss)
7. *G1:* Tiempo Respuesta (Horas) (Escribir en G2 la fórmula de auditoría adjunta abajo)

### 📊 Fórmula de Control de SLA (Celda G2)
Copie y arrastre la siguiente fórmula en la columna G para automatizar los tiempos de respuesta:
excel
=IF(ISBLANK(F2), "Pendiente", (F2 - A2) * 24)


### 🎨 Configuración del Semáforo Visual
Aplique *Formato Condicional* en la columna G con estas tres reglas de negocio:
* *Rojo:* Si la celda es igual a "Pendiente". (Prioridad Máxima de atención).
* *Amarillo:* Si el número es mayor a 24. (Atención fuera de SLA).
* *Verde:* Si el número es menor o igual a 24. (Atención exitosa en menos de un día).

## ⚙️ Instrucciones de Despliegue Técnico

### 1. Despliegue del Webhook (Google Sheets)
1. En su Google Sheets, vaya a Extensiones > Apps Script.
2. Reemplace el editor con el código de webhook/sheets-connector.js.
3. Haga clic en *Implementar > Nueva implementación. Seleccione **Aplicación web*.
4. Configure: Ejecutar como: Su cuenta, Quién tiene acceso: *Cualquiera*.
5. Copia la URL generada.

### 2. Configuración en Dialogflow CX
1. Cree un agente e importe el archivo de la carpeta /dialogflow-agent/.
2. Vaya a Manage > Webhooks, cree uno nuevo llamado Guardar_En_Sheets y pegue la URL de la aplicación web de Google.
3. Asegúrese de que la página Validar_Privacidad redirija al formulario únicamente si el ciudadano acepta los términos legales de la institución.

## ⚙️ Manual de Mantenimiento para Operadores
* *Modificar respuestas:* Vaya a la pestaña *Build* en Dialogflow, seleccione la página correspondiente y edite el texto dentro de *Agent responses*. Guarde los cambios para actualizar WhatsApp de inmediato.
* *Entrenamiento Semanal:* Revise los registros en *Manage > Intent Training* para capturar preguntas no entendidas (No-Match) y asignarlas a sus respectivas intenciones para mejorar la precisión del bot.

## 📄 Licencia
Propiedad exclusiva del *Centro de Servicios Digitales al Ciudadano (CSDC)*. Todos los derechos reservados.
