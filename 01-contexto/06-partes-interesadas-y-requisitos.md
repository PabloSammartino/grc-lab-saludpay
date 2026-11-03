# 06 · Partes interesadas y requisitos legales, regulatorios y contractuales

> **Referencia normativa:** ISO/IEC 27001:2022, cláusula 4.2 (necesidades y expectativas de las partes interesadas) y Anexo A, control 5.31 (requisitos legales, estatutarios, regulatorios y contractuales).

## 1. Partes interesadas

| Parte interesada | Necesidades y expectativas relacionadas con la seguridad | ¿Se aborda en el SGSI? | Cómo |
|---|---|---|---|
| Pacientes | Que sus datos de salud y de pago no se filtren; poder ejercer sus derechos | Sí | Controles de confidencialidad, procedimiento de derechos ARCO |
| Clínicas de Argentina | Plataforma disponible, datos protegidos, cumplimiento de la Ley 25.326 como encargado | Sí | SLA, contrato con anexo de tratamiento de datos |
| Clínicas de EE.UU. | Cumplimiento del BAA y de HIPAA; notificación oportuna de incidentes | Sí | Programa HIPAA, procedimiento de notificación |
| Prepagas y grandes clientes | Certificación ISO 27001, respuesta a cuestionarios de seguridad | Sí | Certificación, paquete de evidencias para clientes |
| AAIP (autoridad de control argentina) | Cumplimiento de la Ley 25.326 | Sí | Registro de bases, medidas de seguridad |
| HHS – Office for Civil Rights (EE.UU.) | Cumplimiento de HIPAA por parte de los *Business Associates* | Sí | Análisis de riesgos HIPAA, salvaguardas |
| Marcas de tarjeta y adquirente | Cumplimiento de PCI DSS | Sí | Validación anual SAQ D proveedores de servicios |
| Directorio y accionistas | Proteger la reputación y el valor de la empresa; cumplir objetivos | Sí | Reportes periódicos del CISO |
| Empleados | Reglas claras, capacitación, protección de sus propios datos | Sí | Políticas, programa de concientización |
| Proveedores críticos | Requisitos de seguridad claros en los contratos | Sí | Gestión de terceros |
| Aseguradora de ciberriesgo | Controles mínimos (MFA, backups, plan de respuesta) para mantener la póliza | Sí | Evidencias de controles |

## 2. Matriz de requisitos legales, regulatorios y contractuales

| ID | Requisito | Fuente | Jurisdicción | Aplica a SaludPay porque… | Responsable interno | Frecuencia de revisión |
|---|---|---|---|---|---|---|
| L-01 | Ley 25.326 de Protección de los Datos Personales y Decreto 1558/2001 | Ley | Argentina | Trata datos personales y de salud de personas en Argentina | Resp. de Protección de Datos | Anual y ante reformas |
| L-02 | Resolución AAIP 47/2018 — medidas de seguridad recomendadas | Regulación | Argentina | Guía para cumplir el art. 9 de la Ley 25.326 | CISO | Anual |
| L-03 | Ley 26.529 de Derechos del Paciente (confidencialidad e intimidad) | Ley | Argentina | Las clínicas clientes están obligadas; SaludPay debe permitirles cumplir | Legales | Anual |
| L-04 | Ley 24.240 de Defensa del Consumidor | Ley | Argentina | Los pacientes son consumidores de un servicio con cobro online | Legales | Anual |
| L-05 | Ley 27.483 — aprobación del Convenio 108 del Consejo de Europa | Tratado | Argentina | Marco internacional de protección de datos ratificado por Argentina | Resp. de Protección de Datos | Ante cambios |
| L-06 | HIPAA Privacy Rule (45 CFR Parte 160 y Parte 164, Subparte E) | Regulación federal | EE.UU. | SaludPay es *Business Associate* de clínicas de EE.UU. | Privacy Officer | Anual |
| L-07 | HIPAA Security Rule (45 CFR Parte 164, Subparte C) | Regulación federal | EE.UU. | Debe proteger la ePHI con salvaguardas administrativas, físicas y técnicas | HIPAA Security Officer (CISO) | Anual y ante la regla nueva |
| L-08 | HIPAA Breach Notification Rule (45 CFR Parte 164, Subparte D) | Regulación federal | EE.UU. | Debe notificar a la clínica sin demora irrazonable y como máximo dentro de los 60 días de descubierta una brecha | CISO | Anual |
| L-09 | Leyes estatales de notificación de brechas (Florida, Texas) | Ley estatal | EE.UU. | Pacientes residentes en esos estados | Legales | Anual |
| C-01 | PCI DSS v4.0.1 | Estándar contractual | Global | Procesa cobros con tarjeta como proveedor de servicios | CISO | Anual (validación) |
| C-02 | Business Associate Agreements (BAA) con cada clínica de EE.UU. | Contrato | EE.UU. | Obligaciones contractuales específicas | Legales | Ante cada firma |
| C-03 | BAA con AWS | Contrato | EE.UU. | AWS almacena ePHI como subcontratista | Legales | Anual |
| C-04 | Contratos de servicio con clínicas (SLA de disponibilidad 99,9%) | Contrato | Argentina / EE.UU. | Compromiso de disponibilidad | COO | Anual |
| C-05 | Póliza de seguro de ciberriesgo | Contrato | Argentina | Exige controles mínimos | CFO | Anual |
| E-01 | ISO/IEC 27001:2022 | Norma voluntaria | Global | Objetivo de certificación | CISO | Continua |
| E-02 | ISO 22301 | Norma voluntaria | Global | Continuidad del negocio (sin certificar) | COO | Anual |

## 3. Seguimiento de cambios normativos

| Tema | Estado (noviembre 2026) | Impacto potencial |
|---|---|---|
| Reforma de la Ley 25.326 | Ley vigente. Hay proyectos de reforma integral en tratamiento en el Congreso (por ejemplo, el expediente 3397-D-2026, presentado en julio de 2026) | Alto: podría incorporar notificación obligatoria de brechas, evaluaciones de impacto y mayores sanciones |
| Actualización de la HIPAA Security Rule | Propuesta publicada en enero de 2025; todavía no es definitiva. HHS movió la fecha objetivo de la regla final a julio de 2027. La regla actual sigue en vigor | Alto: haría obligatorios MFA, cifrado e inventario de activos |
| PCI DSS | v4.0.1 es la única versión activa; el PCI SSC abrió en 2026 un período de comentarios para la próxima versión | Medio |

> 💡 **Nota de aprendizaje:** el monitoreo regulatorio es una tarea permanente del área GRC. En la práctica se suele llevar con suscripciones a boletines oficiales y newsletters especializados, y una revisión trimestral de esta matriz.
