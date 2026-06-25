# Pipeline Command Center

# Pipeline Command Center

🔗 **App en vivo:** https://leoflores0-creator.github.io/pipeline-command-center/

> Tablero para la **gestión, seguimiento y activación del pipeline de ventas** de un Account Manager de cuentas estratégicas: Coverage contra quota, next steps por oportunidad, asignación de tareas al ecosistema (preventas, value engineering, marketing, customer success, partners y BDR) y activación de comunicaciones con el cliente (email, material de marketing y WhatsApp).

**Trabajo Final Integrador** — Diplomatura en IA Aplicada a Entornos Digitales de Gestión · FCE-UBA · Cohorte 2026

---

## El problema

En la venta enterprise, el cuello de botella no siempre es *generar* pipeline, sino **gobernarlo**: saber en todo momento si estás cubierto (el Coverage debe ser un múltiplo de la quota), no perder el *next step* de ninguna oportunidad y coordinar a las muchas personas que intervienen en cada deal. Esa información suele vivir desperdigada entre el CRM, planillas sueltas y la cabeza del vendedor.

## La solución

Una única pantalla —un "command center"— que concentra:

- **Coverage en vivo**, con un semáforo contra el objetivo de cobertura (🔴 <3x · 🟡 3–4x · 🟢 ≥4x).
- **Pipeline en formato Kanban** por etapa, con el ACV de cada oportunidad.
- **Los 3 Whys** de cada deal (*¿por qué hacer algo?*, *¿por qué ahora?*, *¿por qué nosotros?*) con semáforo, bajo la regla del **eslabón más débil**.
- **Calificación MEDDPICC** en el detalle de cada oportunidad.
- **Next steps** ordenados por fecha, resaltando los vencidos.
- **Tareas agrupadas por rol** del ecosistema.
- **Importación desde Salesforce** vía reporte CSV (sin backend, todo en el navegador).
- **Email al asignado**: genera un borrador con el contexto del deal y abre tu cliente de correo.
- **Biblioteca de materiales de MKT** (whitepapers, datasheets, videos, casos de éxito) para adjuntar a las comunicaciones.
- **WhatsApp click-to-chat**: abre WhatsApp con un mensaje personalizado y el link al material.
- **Respuestas pendientes**: seguimiento de los clientes que aún no respondieron, con semáforo por antigüedad.
- Una **capa de IA generativa** que sugiere next steps y redacta briefs para el ecosistema (la IA propone; la persona revisa y aprueba).

> **Control humano por diseño.** La maqueta no envía nada de forma automática: prepara los borradores (email, WhatsApp) y la persona los revisa y envía. Es una decisión deliberada de seguridad y control, no una limitación.

## Para quién es

Para un Account Manager (o cualquier rol comercial con quota) que necesita claridad inmediata sobre su cobertura, disciplina en el seguimiento y rapidez para activar al ecosistema y al cliente, sin depender de informes manuales.

---

## Cómo se usa

1. Abrí `index.html` en cualquier navegador (no requiere instalación, servidor ni base de datos).
2. **Coverage:** el medidor central indica tu cobertura actual y si estás en zona segura.
3. **Kanban:** recorré las oportunidades por etapa. Pasá el cursor sobre los semáforos de los *Whys* para ver el criterio de cada color. Hacé clic en una tarjeta para ver su detalle MEDDPICC y las acciones.
4. **Importar CSV:** botón *Importar CSV* → seleccioná un reporte exportado de Salesforce (ver formato abajo). El tablero se reconstruye con esos datos.
5. **Acciones por oportunidad** (dentro del detalle de cada tarjeta):
   - *Email al asignado:* abre un borrador con el contexto del deal dirigido al rol responsable.
   - *Enviar material:* abre la biblioteca de MKT y permite mandar el material por email o WhatsApp.
   - *WhatsApp al cliente:* abre un mensaje personalizado listo para enviar.
6. **Biblioteca MKT:** botón *Biblioteca MKT* para explorar y filtrar materiales por tipo.
7. **Next steps / Respuestas pendientes:** paneles inferiores para el seguimiento; los vencidos y las respuestas demoradas aparecen en rojo.
8. **Generar con IA:** muestra cómo el asistente generativo propone la próxima acción y un brief para el equipo.

> ⚠️ **Datos ficticios y anonimizados.** Cuentas, montos, contactos y teléfonos son inventados a modo de demostración. No contienen información comercial real.

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

El archivo debe tener una fila de encabezados con estas columnas (ver `datos-ejemplo.csv`):

| Columna | Descripción | Valores |
|---|---|---|
| `cuenta` | Nombre de la cuenta/oportunidad | texto |
| `producto` | Solución ofrecida | texto |
| `acv` | Valor anual del contrato | número |
| `etapa` | Etapa del pipeline | Prospección, Calificación, Validación, Propuesta, Negociación, Cierre |
| `origen` | Fuente del lead | auto, marketing, bdr, partner |
| `cierre` | Fecha estimada de cierre | AAAA-MM-DD |
| `next_step` | Próxima acción | texto |
| `ns_fecha` | Fecha del next step | AAAA-MM-DD |
| `responsable` | Rol asignado | Account Manager, Preventas, Value Engineer, Marketing, Customer Success, Partner, BDR |
| `why_anything` | ¿Por qué hacer algo? | verde, amarillo, rojo |
| `why_now` | ¿Por qué ahora? | verde, amarillo, rojo |
| `why_nosotros` | ¿Por qué nosotros? | verde, amarillo, rojo |
| `cliente` | Nombre del contacto | texto |
| `telefono` | Teléfono del cliente (solo dígitos) | número |
| `respuesta_enviada` | Fecha en que se le escribió (para "respuestas pendientes") | AAAA-MM-DD u vacío |

---

## Cómo desplegarlo (gratis)

Al ser un sitio estático de un solo archivo, se publica en segundos:

- **Netlify:** arrastrá la carpeta del proyecto a [app.netlify.com/drop](https://app.netlify.com/drop), o conectá este repositorio.
- **Vercel:** importá el repositorio desde [vercel.com/new](https://vercel.com/new); detecta el `index.html` automáticamente.
- **GitHub Pages:** activá Pages en *Settings → Pages → Branch: main*.

---

## Herramientas de IA generativa utilizadas

| Parte del proyecto | Herramienta | Rol |
|---|---|---|
| Diseño y código del tablero (front-end) | Claude (Anthropic) | Generación del HTML/CSS/JS bajo dirección del autor |
| Capa generativa de next steps y briefs | GPT / Proyecto de Claude | Asistente que sugiere acciones; la decisión final es humana |
| Ideación y estructura del trabajo | Modelo de IA generativa | Brainstorming del enfoque |

El detalle de prompts, decisiones y ajustes está documentado en el **informe en PDF** que acompaña a este repositorio. Las instrucciones del asistente generativo están versionadas en la carpeta `cerebro/`.

---

## Versiones

El proyecto se desarrolla de forma iterativa; el historial de *commits* refleja su evolución.

- **v1** — Tablero funcional con Coverage, Kanban, 3 Whys, MEDDPICC, next steps y panel de ecosistema.
- **v2** — Cerebro generativo (`cerebro/`): instrucciones y ejemplos del asistente.
- **v3** — Importación CSV de Salesforce, email al asignado, biblioteca de materiales de MKT, WhatsApp click-to-chat y panel de respuestas pendientes (todo como maqueta sin backend).
- *(próximas)* — Automatización real de envíos e integración en vivo vía n8n/APIs.

---

## Estructura del repositorio

```
pipeline-command-center/
├── index.html          # la app (v3)
├── datos-ejemplo.csv   # CSV de ejemplo para la importación
├── README.md
└── cerebro/
    ├── instrucciones.md
    └── ejemplos-de-uso.md
```

---

## Autor

Leonardo Flores · Cohorte 2026 · FCE-UBA · ID [57FL25142673@campus.economicas.uba.ar](mailto:57FL25142673@campus.economicas.uba.ar)
