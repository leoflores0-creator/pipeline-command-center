# Pipeline Command Center

> Tablero para la **gestión y seguimiento del pipeline de ventas** de un Account Manager de cuentas estratégicas: Coverage contra quota, next steps por oportunidad y asignación de tareas al ecosistema (preventas, value engineering, marketing, customer success, partners y BDR).

**Trabajo Final Integrador** — Diplomatura en IA Aplicada a Entornos Digitales de Gestión · FCE-UBA · Cohorte 2026

---

## El problema

En la venta enterprise, el cuello de botella no siempre es *generar* pipeline, sino **gobernarlo**: saber en todo momento si estás cubierto (el Coverage debe ser un múltiplo de la quota), no perder el *next step* de ninguna oportunidad y coordinar a las muchas personas que intervienen en cada deal. Esa información suele vivir desperdigada entre el CRM, planillas sueltas y la cabeza del vendedor.

## La solución

Una única pantalla —un "command center"— que concentra:

- **Coverage en vivo**, con un semáforo contra el objetivo de cobertura.
- **Pipeline en formato Kanban** por etapa, con el ACV de cada oportunidad.
- **Los 3 Whys** de cada deal (*¿por qué hacer algo?*, *¿por qué ahora?*, *¿por qué BMC?*) con semáforo, bajo la regla del **eslabón más débil**: la salud del deal es igual a su Why más flojo.
- **Calificación MEDDPICC** en el detalle de cada oportunidad.
- **Next steps** ordenados por fecha, resaltando los vencidos.
- **Tareas agrupadas por rol** del ecosistema.
- Una **capa de IA generativa** que sugiere next steps y redacta briefs para el ecosistema (la IA propone; la persona revisa y aprueba).

## Para quién es

Para un Account Manager (o cualquier rol comercial con quota) que necesita claridad inmediata sobre su cobertura y disciplina en el seguimiento, sin depender de informes manuales.

---

## Cómo se usa

1. Abrí `index.html` en cualquier navegador (no requiere instalación, servidor ni base de datos).
2. **Coverage:** el medidor central indica tu cobertura actual y si estás en zona segura.
3. **Kanban:** recorré las oportunidades por etapa. Pasá el cursor sobre los semáforos de los *Whys* para ver el criterio de cada color. Hacé clic en una tarjeta para ver su detalle MEDDPICC.
4. **Next steps:** revisá las acciones pendientes; las vencidas aparecen en rojo.
5. **Ecosistema:** mirá cómo se reparten las tareas entre los distintos roles.
6. **Generar con IA:** abre una muestra de cómo el asistente generativo propone la próxima acción y un brief para el equipo.

> ⚠️ **Datos ficticios y anonimizados.** Las cuentas, montos y oportunidades son inventados a modo de demostración. No contienen información comercial real.

### Configuración

Toda la lógica de negocio es editable en un solo lugar, dentro de `index.html`, en el objeto `CONFIG`:

```js
const CONFIG = {
  quota: 1500000,                      // quota anual en ACV
  coverageBands: { red: 3, green: 4 }, // 🔴 <3x · 🟡 3–4x · 🟢 ≥4x
  today: new Date('2026-06-24')
};
```

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
| Capa generativa de next steps y briefs | GPT / Proyecto de Claude *(en desarrollo)* | Asistente que sugiere acciones; la decisión final es humana |
| Ideación y estructura del trabajo | Modelo de IA generativa | Brainstorming del enfoque |

El detalle de prompts, decisiones y ajustes está documentado en el **informe en PDF** que acompaña a este repositorio.

---

## Versiones

El proyecto se desarrolla de forma iterativa; el historial de *commits* refleja su evolución.

- **v1** — Tablero funcional con Coverage, Kanban, 3 Whys, MEDDPICC, next steps y panel de ecosistema. Capa de IA como demostración.
- *(próximas)* — Integración real del asistente generativo, edición de datos, persistencia.

---

## Autor

Leonardo Flores · Cohorte 2026 · FCE-UBA
ID 57FL25142673@campus.economicas.uba.ar
