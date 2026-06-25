# Cerebro — Ejemplos de uso

Casos de prueba para validar el asistente y para documentar en la sección **Metodología** del informe. Muestran dos comportamientos clave: que **pide información cuando faltan datos** y que **produce una salida estructurada y accionable** cuando los tiene.

---

## Ejemplo 1 — Notas incompletas (el asistente repregunta)

**Entrada del vendedor:**
> Tuve una primera reunión con una empresa de retail. Les interesa nuestra plataforma de automatización. Quedaron en pensarlo.

**Salida esperada del asistente:**
> Antes de calificar necesito tres datos:
> 1. ¿Qué problema concreto te mencionaron, y alguien lo cuantificó (costo, tiempo, riesgo)?
> 2. ¿Hay algún evento o fecha que los empuje a decidir, o es interés general?
> 3. ¿Con quién hablaste y esa persona tiene poder de decisión o presupuesto?
>
> Con eso te devuelvo la calificación de los 3 Whys, el next step y a quién del ecosistema conviene sumar.

*Por qué importa: demuestra el control de calidad —la IA no inventa una calificación sobre aire— y mantiene al vendedor en el centro.*

---

## Ejemplo 2 — Notas completas (salida estructurada)

**Entrada del vendedor:**
> Cuenta de telco. Reunión con el Director de IT y el sponsor técnico. Hoy procesan cierres manualmente y calculan que pierden ~40 horas/mes del equipo, que el sponsor valuó en plata. Tienen una auditoría regulatoria en septiembre que los obliga a automatizar. El sponsor está convencido de ir con nosotros y quiere ayudarnos a vender adentro, pero el Director todavía compara con un competidor. Deal estimado en 900K ACV, etapa de propuesta.

**Salida esperada del asistente:**

> **1. Resumen del deal**
> Telco · Plataforma de Automatización · ~900K ACV · etapa: Propuesta.
>
> **2. Calificación 3 Whys**
> - ¿Por qué hacer algo? 🟢 — Dolor cuantificado (≈40 h/mes valuadas por el sponsor).
> - ¿Por qué ahora? 🟢 — Compelling event con fecha: auditoría regulatoria de septiembre.
> - ¿Por qué BMC? 🟡 — Tenés champion (el sponsor vende adentro), pero el economic buyer todavía compara con un competidor. *Para subir a verde:* ganar los criterios de decisión frente al Director de IT.
>
> **3. Salud del deal**
> 🟡 Amarillo. Los dos primeros Whys son sólidos; el deal se define en el "por qué BMC".
>
> **4. MEDDPICC**
> Cubiertos: Metrics, Identify pain, Champion, Compelling event. Faltan: Decision criteria explícitos, confirmación del Economic buyer y mapa del Competition.
>
> **5. Next step recomendado**
> Agendar una sesión de "decision criteria" con el Director de IT para fijar, junto a él, los criterios de evaluación y posicionarlos a tu favor. **Responsable:** Account Manager. **Fecha objetivo:** dentro de 7 días.
>
> **6. Briefs para el ecosistema**
> → **Value Engineer:** "Necesito un caso de negocio para la telco (900K ACV) usando el dato del sponsor de ~40 h/mes y la auditoría de septiembre como driver. ¿Podés armar el ROI y 2–3 métricas de impacto para la reunión con el Director de IT?"
> → **Preventas:** "Preparemos una comparativa técnica honesta frente a [competidor] enfocada en los criterios que más le pesan al Director."
>
> **7. Banderas de riesgo**
> El champion no alcanza si el economic buyer no está convencido. Riesgo de empate técnico con el competidor: hay que diferenciar en criterios, no en features.

*Por qué importa: la salida espeja exactamente las secciones del tablero (3 Whys, MEDDPICC, next step, ecosistema), de modo que el cerebro y el Command Center hablan el mismo idioma.*
