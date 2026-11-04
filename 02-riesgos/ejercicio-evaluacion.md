# ✍️ Ejercicio · Evaluación de riesgos R-03 a R-08

Tu tarea como analista GRC: evaluar seis riesgos usando la [metodología](01-metodologia.md). Los escenarios, las vulnerabilidades y los controles existentes ya están en el [registro](registro-riesgos.csv). Usá **R-01 y R-02 como modelo**.

## Cómo hacerlo

Para cada riesgo completá:

1. **Probabilidad e impacto inherentes** (sin ningún control) → multiplicá → nivel.
2. **Probabilidad e impacto residuales** (con los controles existentes) → multiplicá → nivel.
3. **Tratamiento** según el apetito de riesgo (sección 7 de la metodología).
4. **Dos o tres acciones concretas.**
5. **Una línea de justificación** de los números. Es lo más importante: en una auditoría o entrevista te van a preguntar "¿por qué un 4 y no un 3?".

Para el impacto, recordá revisar las **cinco dimensiones** y quedarte con la más alta.

No te preocupes por los controles del Anexo A: los agregamos juntos en la corrección.

---

### R-03 · Soporte que consulta fichas sin justificación — ✅ resuelto (ver registro)

| | Probabilidad | Impacto | Riesgo | Nivel |
|---|---|---|---|---|
| Inherente | | | | |
| Residual | | | | |

- **Justificación:**
- **Tratamiento:**
- **Acciones:**

> 🤔 Pista: ¿la VPN con MFA reduce este riesgo? ¿Quién es la amenaza acá: alguien de afuera o alguien que ya está adentro?

---

### R-04 · Skimming en la página de checkout — ✅ resuelto (ver registro)

| | Probabilidad | Impacto | Riesgo | Nivel |
|---|---|---|---|---|
| Inherente | | | | |
| Residual | | | | |

- **Justificación:**
- **Tratamiento:**
- **Acciones:**

> 🤔 Pista: SaludPay nunca ve el número de tarjeta. ¿Eso cambia el impacto para los pacientes y frente a PCI DSS?

---

### R-05 · Fuga por exportación CSV — ✅ resuelto (ver registro)

| | Probabilidad | Impacto | Riesgo | Nivel |
|---|---|---|---|---|
| Inherente | | | | |
| Residual | | | | |

- **Justificación:**
- **Tratamiento:**
- **Acciones:**

> 🤔 Pista: ¿quién es el **responsable** de esos datos según la Ley 25.326 y quién el **encargado**? ¿Hay alguna opción además de "mitigar"?

---

### R-06 · Caída de la región de AWS — ✅ resuelto (ver registro)

| | Probabilidad | Impacto | Riesgo | Nivel |
|---|---|---|---|---|
| Inherente | | | | |
| Residual | | | | |

- **Justificación:**
- **Tratamiento:**
- **Acciones:**

> 🤔 Pista: los backups en otra región, ¿reducen la probabilidad de que AWS se caiga o el impacto si se cae?

---

### R-07 · Phishing con robo de credenciales

| | Probabilidad | Impacto | Riesgo | Nivel |
|---|---|---|---|---|
| Inherente | | | | |
| Residual | | | | |

- **Justificación:**
- **Tratamiento:**
- **Acciones:**

> 🤔 Pista: ¿el MFA por SMS protege igual que una llave física o una app de autenticación frente a una página clonada?

---

### R-08 · Notificación tardía de una brecha HIPAA

| | Probabilidad | Impacto | Riesgo | Nivel |
|---|---|---|---|---|
| Inherente | | | | |
| Residual | | | | |

- **Justificación:**
- **Tratamiento:**
- **Acciones:**

> 🤔 Pista: acá la amenaza no es un hacker, es la propia organización. Revisá la regla especial de la sección 7 de la metodología.
