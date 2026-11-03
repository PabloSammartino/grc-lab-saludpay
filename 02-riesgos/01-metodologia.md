# 01 · Metodología de gestión de riesgos

> **Referencias normativas:** ISO/IEC 27001:2022, cláusulas 6.1.2 (evaluación de riesgos), 6.1.3 (tratamiento), 8.2 y 8.3 · ISO 31000:2018 · ISO/IEC 27005:2022 · HIPAA Security Rule §164.308(a)(1)(ii)(A) y (B) (análisis y gestión de riesgos) · PCI DSS v4.0.1, requisito 12.3.1 (análisis de riesgos específicos).
> **Versión:** 1.0 · **Estado:** Borrador · **Elaborado por:** Analista GRC · **Aprueba:** CISO

## 1. Objetivo

Definir un método **repetible y comparable** para identificar, analizar, evaluar y tratar los riesgos de seguridad de la información y de privacidad de SaludPay. ISO 27001 exige que la evaluación produzca "resultados consistentes, válidos y comparables" (cl. 6.1.2 b): por eso las escalas están definidas con criterios concretos y no se dejan a la intuición de cada evaluador.

## 2. Enfoque

Se usa un enfoque **basado en activos y escenarios**:

```
ACTIVO  +  AMENAZA  +  VULNERABILIDAD  →  ESCENARIO DE RIESGO  →  PROBABILIDAD × IMPACTO
```

| Concepto | Definición | Ejemplo |
|---|---|---|
| **Activo** | Lo que hay que proteger (del [inventario](../01-contexto/04-inventario-activos.csv)) | A-001 Base de datos de pacientes AR |
| **Amenaza** | Lo que puede causar daño | Grupo criminal con ransomware |
| **Vulnerabilidad** | La debilidad que la amenaza aprovecha | Backups accesibles con las mismas credenciales que producción |
| **Escenario** | La historia completa en una oración | "Un atacante obtiene credenciales de infraestructura, cifra la base de pacientes y los backups, y la plataforma queda inoperativa" |

> 💡 **Regla práctica:** si el escenario no se puede contar como una historia con un "quién", un "cómo" y un "qué pasa después", está mal formulado. "Riesgo de ciberataque" no es un riesgo: es una categoría.

## 3. Escala de probabilidad

| Valor | Nivel | Criterio |
|---|---|---|
| 1 | Muy baja | No se espera que ocurra en los próximos 5 años; no hay antecedentes en el sector |
| 2 | Baja | Podría ocurrir una vez en 3–5 años; hay antecedentes aislados en el sector |
| 3 | Media | Podría ocurrir una vez en 1–3 años; es frecuente en el sector |
| 4 | Alta | Probable dentro del año; ya ocurrió en SaludPay o la vulnerabilidad es conocida y fácil de explotar |
| 5 | Muy alta | Ocurre o se espera que ocurra varias veces por año |

## 4. Escala de impacto

El impacto se evalúa en **cinco dimensiones**. Se toma el **valor más alto** (criterio conservador: un riesgo con impacto legal grave es grave aunque no cueste dinero en lo inmediato).

| Valor | Operativo (disponibilidad) | Pacientes / titulares | Legal y regulatorio | Financiero | Reputacional |
|---|---|---|---|---|---|
| 1 · Insignificante | Caída < 1 h fuera del horario de atención | Sin afectación | Sin incumplimiento | < USD 5.000 | Sin trascendencia externa |
| 2 · Menor | Caída < 4 h | Datos no sensibles de < 100 personas | Incumplimiento formal menor, sin sanción probable | USD 5.000–50.000 | Quejas aisladas de clientes |
| 3 · Moderado | Caída de 4–24 h | Datos no sensibles masivos o sensibles de < 100 personas | Posible sanción leve (AAIP) o incumplimiento contractual | USD 50.000–250.000 | Pérdida de algún cliente; prensa especializada |
| 4 · Mayor | Caída de 1–3 días | Datos de salud de 100–10.000 personas | Sanción grave, notificación HIPAA a HHS, pérdida de certificación | USD 250.000–1 M | Pérdida de varios clientes; prensa general |
| 5 · Catastrófico | Caída > 3 días o pérdida de datos | Datos de salud de > 10.000 personas o daño a la salud de un paciente | Suspensión de actividad, acciones colectivas, prohibición de procesar tarjetas | > USD 1 M | Daño que pone en riesgo la continuidad de la empresa |

## 5. Cálculo y matriz de riesgo

**Nivel de riesgo = Probabilidad × Impacto** (valores de 1 a 25)

| Probabilidad ↓ / Impacto → | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| **5** | 🟨 5 | 🟧 10 | 🟥 15 | 🟥 20 | 🟥 25 |
| **4** | 🟩 4 | 🟨 8 | 🟧 12 | 🟥 16 | 🟥 20 |
| **3** | 🟩 3 | 🟨 6 | 🟨 9 | 🟧 12 | 🟥 15 |
| **2** | 🟩 2 | 🟩 4 | 🟨 6 | 🟨 8 | 🟧 10 |
| **1** | 🟩 1 | 🟩 2 | 🟩 3 | 🟩 4 | 🟨 5 |

| Rango | Nivel |
|---|---|
| 1–4 | 🟩 **Bajo** |
| 5–9 | 🟨 **Medio** |
| 10–14 | 🟧 **Alto** |
| 15–25 | 🟥 **Crítico** |

## 6. Riesgo inherente y residual

- **Riesgo inherente:** el nivel de riesgo **si no existiera ningún control**. Sirve para saber cuánto "trabajo" hacen los controles actuales.
- **Riesgo residual:** el nivel de riesgo **considerando los controles que hoy existen y funcionan**. Es el que se compara con el apetito de riesgo.

Un control solo baja el riesgo residual si **existe evidencia** de que funciona. Un control "que está en un documento pero nadie aplica" no cuenta.

Los controles suelen reducir **la probabilidad** (ej.: MFA hace más difícil robar una cuenta) o **el impacto** (ej.: un backup probado acorta la caída). Al evaluar el residual, pensá cuál de los dos baja cada control.

## 7. Apetito de riesgo y criterios de aceptación

Aprobados por el Directorio (cl. 6.1.2 a de ISO 27001):

| Nivel residual | Decisión | Quién puede aceptarlo | Plazo para tratarlo |
|---|---|---|---|
| 🟩 Bajo | Se acepta y se monitorea en la revisión anual | Dueño del riesgo | — |
| 🟨 Medio | Se acepta con justificación **o** se trata | Dueño del riesgo + CISO | 12 meses si se trata |
| 🟧 Alto | **Debe tratarse.** Aceptación solo excepcional | CEO | 90 días |
| 🟥 Crítico | **Tratamiento inmediato** y escalamiento al Directorio | No se acepta | 30 días para medidas iniciales |

**Regla especial:** ningún riesgo que implique un **incumplimiento legal** (Ley 25.326, HIPAA) puede aceptarse sin tratar, cualquiera sea su nivel.

## 8. Opciones de tratamiento

| Opción | Qué significa | Ejemplo en SaludPay |
|---|---|---|
| **Mitigar** | Aplicar controles para reducir probabilidad o impacto | Implementar MFA, cifrado, backups inmutables |
| **Transferir** | Compartir el impacto con un tercero | Seguro de ciberriesgo; tokenización con la pasarela de pagos |
| **Evitar** | Dejar de hacer la actividad que genera el riesgo | Eliminar la exportación CSV del panel |
| **Aceptar** | Asumir el riesgo conscientemente, dentro del apetito | Riesgo bajo de caída de un sistema interno no crítico |

> ⚠️ Transferir **no elimina** la responsabilidad legal: si el proveedor de mensajería filtra datos, ante la clínica y la AAIP responde SaludPay.

Cada tratamiento se vincula con **controles del Anexo A de ISO 27001:2022**, que alimentan la Declaración de Aplicabilidad (Fase 3).

## 9. Roles

| Rol | Responsabilidad |
|---|---|
| **Analista GRC** | Facilita las evaluaciones, mantiene el registro, prepara los reportes |
| **Dueño del riesgo** | Persona con autoridad para decidir el tratamiento y aceptar el residual (normalmente el dueño del activo principal) |
| **CISO** | Valida las evaluaciones, propone controles, escala riesgos altos y críticos |
| **Dirección** | Aprueba el apetito de riesgo y acepta excepciones |

## 10. Frecuencia de revisión

- **Evaluación completa:** una vez por año (también cumple con el análisis de riesgos que exige HIPAA).
- **Revisión puntual:** ante cambios significativos (nuevo producto, nuevo país, nuevo proveedor crítico, cambio de arquitectura), incidentes graves o cambios normativos.
- **Seguimiento del plan de tratamiento:** mensual en el comité de seguridad.

## 11. Registro

El registro de riesgos se mantiene en [`registro-riesgos.csv`](registro-riesgos.csv). Columnas:

| Columna | Contenido |
|---|---|
| `id` | R-01, R-02… |
| `activos` | IDs del inventario afectados |
| `amenaza` / `vulnerabilidad` / `escenario` | Según la sección 2 |
| `dueno_riesgo` | Según la sección 9 |
| `marcos` | Normas involucradas |
| `p_inh` / `i_inh` / `riesgo_inh` / `nivel_inh` | Evaluación inherente |
| `controles_existentes` | Solo los que tienen evidencia |
| `p_res` / `i_res` / `riesgo_res` / `nivel_res` | Evaluación residual |
| `tratamiento` | Mitigar / Transferir / Evitar / Aceptar |
| `acciones` | Qué se va a hacer |
| `controles_anexo_a` | Controles ISO 27001:2022 relacionados |
| `responsable` / `fecha_objetivo` / `estado` | Seguimiento |
