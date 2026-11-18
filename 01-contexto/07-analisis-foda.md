# 07 · Análisis FODA de seguridad de la información

> **Referencia normativa:** ISO/IEC 27001:2022, cláusula 4.1 (comprensión de la organización y su contexto).
> **Versión:** 1.0 · **Estado:** Borrador · **Elaborado por:** Analista GRC

## 1. Objetivo

Resumir el contexto interno y externo de SaludPay desde la perspectiva de la seguridad de la información y el cumplimiento normativo. El análisis complementa la [descripción de la organización](01-descripcion-empresa.md) y se valida contra el [registro de riesgos](../02-riesgos/registro-riesgos.csv).

- **Fortalezas y debilidades:** factores **internos**, que la organización controla.
- **Oportunidades y amenazas:** factores **externos**, propios del entorno.

## 2. Matriz FODA

### 💪 Fortalezas

1. **Pagos tokenizados:** los datos de tarjeta nunca pasan por los servidores de SaludPay, lo que reduce mucho el alcance de PCI DSS.
2. **Compromiso de la Dirección:** decidió certificar ISO 27001, cuenta con un CISO que reporta al CEO y con un responsable de protección de datos.
3. **Infraestructura 100% cloud en AWS,** con cifrado, alertas de seguridad y base de datos en varias zonas de disponibilidad.
4. **Minimización ya aplicada en parte:** los recordatorios no revelan la especialidad ni el motivo de consulta.
5. **Cultura ágil con CI/CD:** permite implementar controles técnicos rápidamente una vez decididos.

### ⚠️ Debilidades

1. **Procesos de seguridad poco documentados,** creados sobre la marcha, con un equipo de seguridad de solo dos personas.
2. **Gestión de accesos débil:** soporte ve todos los pacientes, hay claves de AWS sin MFA y el segundo factor del correo es por SMS (R-01, R-03, R-07).
3. **Falta de registros:** no queda constancia de qué fichas se consultan ni de quién exporta datos (R-03, R-05).
4. **Brechas legales:** transferencias internacionales sin respaldo, contratos sin cláusula de encargado del tratamiento y sin procedimiento de notificación de brechas (R-02, R-08).
5. **Resiliencia sin probar:** la plataforma corre en una sola región, la restauración de backups nunca se probó y no existe un plan de recuperación (R-01, R-06).

### 🚀 Oportunidades

1. **La certificación ISO 27001 como diferencial comercial** en licitaciones con prepagas y grandes clientes.
2. **Crecimiento en EE.UU.:** demostrar cumplimiento HIPAA facilita sumar clínicas en un mercado en expansión.
3. **Anticiparse a la reforma de la Ley 25.326:** si la nueva ley se acerca al estándar europeo (RGPD), quien ya cumpla tendrá ventaja frente a la competencia.
4. **Herramientas de seguridad accesibles:** passkeys y llaves FIDO2 en Google Workspace y servicios nativos de AWS permiten mejorar mucho a bajo costo.
5. **Clientes que piden cada vez más cuestionarios de seguridad:** contar con un paquete de evidencias listo acelera las ventas.

### 🌪️ Amenazas

1. **El sector salud es blanco prioritario del ransomware** a nivel mundial.
2. **Ataques a la cadena de suministro:** scripts de terceros en la página de pago y proveedores SaaS comprometidos (R-04).
3. **Cambios regulatorios:** la reforma de la Ley 25.326 y la actualización propuesta de la HIPAA Security Rule (que haría obligatorios el MFA y el cifrado) pueden abrir brechas de cumplimiento.
4. **Dependencia de proveedores críticos:** una falla o un incidente en AWS, la pasarela de pagos o la mensajería impacta directamente en SaludPay (R-06).
5. **Phishing cada vez más sofisticado,** potenciado por IA generativa, y fraude por correo corporativo comprometido (R-07).

## 3. FODA cruzado: estrategias

Un FODA aislado es una foto del contexto. Cruzar los cuadrantes permite derivar estrategias:

| Cruce | Pregunta | Estrategia para SaludPay |
|---|---|---|
| **F + O** (ofensiva) | ¿Cómo uso mis fortalezas para aprovechar oportunidades? | Apoyarse en el compromiso de la Dirección para certificar ISO 27001 y usar la certificación en las licitaciones |
| **D + O** (reorientación) | ¿Cómo uso las oportunidades para corregir debilidades? | Usar las passkeys de Google Workspace para resolver el MFA débil a bajo costo |
| **F + A** (defensiva) | ¿Cómo uso mis fortalezas para frenar amenazas? | Aprovechar la tokenización y el CI/CD para blindar rápidamente la página de pago |
| **D + A** (supervivencia) | ¿Qué debilidad, combinada con qué amenaza, puede poner en riesgo a la empresa? | Accesos débiles + ransomware: es el escenario del riesgo R-01, el crítico más grave |

## 4. Relación con la gestión de riesgos

El cuadrante **Debilidades + Amenazas** reproduce los riesgos críticos del [registro de riesgos](../02-riesgos/registro-riesgos.csv). Esa coincidencia valida ambos análisis: el FODA ofrece la mirada estratégica y el registro de riesgos, el detalle operativo para tratarlos.

| Debilidad | Amenaza | Riesgo del registro |
|---|---|---|
| Gestión de accesos débil | Ransomware en el sector salud | R-01 · Ransomware |
| Gestión de accesos débil | Phishing sofisticado | R-07 · Phishing |
| Falta de registros | — (amenaza interna) | R-03 · Soporte, R-05 · Exportación |
| Brechas legales | Cambios regulatorios | R-02 · Logs a EE.UU., R-08 · Notificación tardía |
| Resiliencia sin probar | Dependencia de proveedores | R-06 · Caída de AWS |
