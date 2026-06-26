# Pipeline Command Center

🔗 **App en vivo:** https://leoflores0-creator.github.io/pipeline-command-center/

> Tablero para la **gestión, seguimiento y activación del pipeline de ventas** de un Account Manager de cuentas estratégicas: Coverage contra quota, next steps por oportunidad, histórico de cada cuenta, calificación (MEDDPICC y los 3 Whys), asignación de tareas al ecosistema y activación de comunicaciones con el cliente (email, materiales de marketing y WhatsApp).

**Trabajo Final Integrador** — Diplomatura en IA Aplicada a Entornos Digitales de Gestión · FCE-UBA · Cohorte 2026

---

## El problema

En la venta enterprise, el cuello de botella no siempre es *generar* pipeline, sino **darle progreso**: saber en todo momento si se está cubierto (el Coverage debe ser un múltiplo de la quota), no perder el *next step* de ninguna oportunidad y coordinar a las muchas personas que intervienen en cada deal. Esa información suele vivir dispersa entre el CRM, planillas sueltas y la cabeza del vendedor, y cuando no está visible el pipeline se diluye: se pierde el momentum, los mails se responden tarde, los compromisos no se cumplen y las tareas asignadas al ecosistema se pierden.

## La solución

Una única pantalla —un *command center*— que concentra:

- **Coverage en vivo** contra la quota, con semáforo y objetivo con colchón (🔴 <3x · 🟡 3–4x · 🟢 ≥4x), y la distinción entre pipe total y pipe generado por el vendedor.
- **Pipeline en formato Kanban** por etapa, con el valor (ACV) de cada oportunidad.
- **Calificación por los 3 Whys** (¿por qué hacer algo?, ¿por qué ahora?, ¿por qué nosotros?) con semáforo y la regla del eslabón más débil.
- **MEDDPICC con detalle**: al pinchar cada elemento completado se ve qué se declaró (métricas, economic buyer, champion, etc., con nombre y cargo del contacto).
- **Histórico de cada oportunidad**: acciones realizadas en línea de tiempo y acciones pendientes **accionables** (disparan email, material o WhatsApp, o se marcan como realizadas).
- **Paneles de next steps** (con los vencidos resaltados) y de **respuestas pendientes** del cliente (con semáforo por antigüedad).
- **Asignación y seguimiento de tareas por rol del ecosistema** (preventas, value engineering, marketing, customer success, partners y BDR).
- **Capa de activación**: importación de datos por CSV (reporte de Salesforce), borradores de email al asignado, biblioteca de materiales de marketing y mensajes de WhatsApp *click-to-chat*.
- **Selector de vendedores** (vista por cartera) y un **asistente de IA** (demostración del “cerebro”) que sugiere next steps y briefs.

> **Control humano por diseño.** La maqueta no envía nada de forma automática: prepara los borradores y la persona los revisa y envía. Es una decisión deliberada de seguridad y control.

## Para quién es

Para un Account Manager (o cualquier rol comercial con quota) que necesita claridad inmediata sobre su cobertura, disciplina en el seguimiento y rapidez para activar al ecosistema y al cliente, sin depender de informes manuales.

---

## Cómo se usa

1. Abrí la [app en vivo](https://leoflores0-creator.github.io/pipeline-command-center/) (o `index.html` en cualquier navegador; no requiere instalación ni servidor).
2. **Selector de vendedor** (arriba): cambiá de cartera; el Coverage, el Kanban y los paneles se recalculan.
3. **Coverage:** el medidor central indica la cobertura actual y si se está en zona segura.
4. **Kanban:** recorré las oportunidades por etapa. Pasá el cursor sobre los semáforos de los *Whys* para ver el criterio de cada color. Hacé clic en una tarjeta para ver su detalle.
5. **Detalle de la oportunidad:** los 3 Whys, el MEDDPICC (tocá una letra en verde para ver qué se declaró), el histórico de acciones realizadas y las pendientes accionables.
6. **Importar CSV:** botón *Importar CSV* → seleccioná un reporte exportado de Salesforce (ver formato abajo).
7. **Acciones:** desde cada oportunidad podés generar un borrador de email al asignado, enviar material de marketing o un WhatsApp al cliente.
8. **Generar con IA:** muestra cómo el asistente generativo propone el próximo paso y un brief (demostración del cerebro).

> ⚠️ **Datos ilustrativos.** Las empresas son reales, pero los contactos, montos y datos de pipeline son **ficticios**; los nombres de las personas son inventados y no corresponden a ejecutivos reales.

### Configuración

Toda la lógica de negocio es editable en un solo lugar, dentro de `index.html`, en el objeto `CONFIG`:

```js
const CONFIG = {
  quota: 1500000,                      // quota anual en ACV
  coverageBands: { red: 3, green: 4 }, // 🔴 <3x · 🟡 3–4x · 🟢 ≥4x
  today: new Date('2026-06-24')
};
```

### Formato del CSV (importación desde Salesforce)

El archivo debe tener una fila de encabezados con estas columnas (ver `datos-ejemplo.csv`): `cuenta`, `producto`, `acv`, `etapa`, `origen`, `cierre`, `next_step`, `ns_fecha`, `responsable`, `why_anything`, `why_now`, `why_nosotros`, `cliente`, `telefono`, `respuesta_enviada`. Los semáforos de los Whys aceptan `verde` / `amarillo` / `rojo`; las etapas son Prospección, Calificación, Validación, Propuesta, Negociación, Cierre; y las fechas van en formato AAAA-MM-DD.

---

## Arquitectura objetivo (en producción)

La maqueta es la versión sin backend. En producción, **n8n** actúa como capa central de integración y automatización: sincroniza el pipeline con Salesforce, opera como backend del cerebro de IA (invoca la API de Claude) y, tras la aprobación del vendedor, ejecuta la activación por email, WhatsApp y el repositorio de marketing.

![Arquitectura objetivo en producción](diagramas/arquitectura.png)

### Flujos en n8n

**Sincronización con Salesforce** — trae las oportunidades del CRM y actualiza la app de forma periódica.

![Flujo n8n — Salesforce](diagramas/n8n-salesforce.png)

**Cerebro de IA** — recibe las notas de la oportunidad, llama a la API de Claude con las instrucciones del asistente y devuelve next steps y briefs.

![Flujo n8n — Cerebro](diagramas/n8n-cerebro.png)

**Activación** — tras la aprobación humana, envía por email o WhatsApp, adjunta el material y registra la actividad en Salesforce.

![Flujo n8n — Activación](diagramas/n8n-activacion.png)

---

## Cómo desplegarlo (gratis)

Al ser un sitio estático de un solo archivo, se publica en segundos:

- **GitHub Pages:** *Settings → Pages → Branch: main → /(root)*. (Es como está publicada la app en vivo.)
- **Netlify:** arrastrá la carpeta a [app.netlify.com/drop](https://app.netlify.com/drop).
- **Vercel:** importá el repositorio desde [vercel.com/new](https://vercel.com/new).

---

## Herramientas de IA generativa utilizadas

| Parte del proyecto | Herramienta | Rol |
|---|---|---|
| Diseño y código del tablero (front-end) | Claude (Anthropic) | Generación del HTML/CSS/JS bajo dirección del autor (vibe coding) |
| Capa generativa de next steps y briefs | Proyecto de Claude (el “cerebro”) | Asistente que sugiere acciones; la decisión final es humana |
| Versionado y publicación | GitHub + GitHub Pages | Historial del proceso y app en vivo |

Las instrucciones del asistente generativo están versionadas en la carpeta `cerebro/`. El detalle del proceso, los prompts y el análisis están en el **informe en PDF** que acompaña a la entrega.

---

## Versiones

El proyecto se desarrolló de forma iterativa; el historial de *commits* refleja su evolución: tablero funcional (Coverage, Kanban, 3 Whys, MEDDPICC) → cerebro generativo → capa de activación (CSV, email, materiales, WhatsApp) → histórico accionable y MEDDPICC con detalle → empresas reales y selector de vendedores → despersonalización y publicación en vivo.

---

## Estructura del repositorio

```
pipeline-command-center/
├── index.html              # la app
├── datos-ejemplo.csv       # CSV de ejemplo para la importación
├── README.md
├── cerebro/
│   ├── instrucciones.md
│   └── ejemplos-de-uso.md
└── diagramas/
    ├── arquitectura.png
    ├── n8n-salesforce.png
    ├── n8n-cerebro.png
    └── n8n-activacion.png
```

---

## Autor

Leonardo Flores · Cohorte 2026 · FCE-UBA · ID [57FL25142673@campus.economicas.uba.ar](mailto:57FL25142673@campus.economicas.uba.ar)
