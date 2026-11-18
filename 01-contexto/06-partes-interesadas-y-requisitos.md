# 06 · Partes interesadas y requisitos legales, regulatorios y contractuales

> **Referencia normativa:** ISO/IEC 27001:2022, cláusula 4.2 (necesidades y expectativas de las partes interesadas) y Anexo A, control 5.31 (requisitos legales, estatutarios, regulatorios y contractuales).

## 1. Partes interesadas

**Criterios de la tabla:**
- **Expectativa:** lo que la parte espera, aunque no esté escrito (ej.: "que mis datos estén seguros").
- **Requisito:** lo que es exigible por ley, contrato o norma (ej.: "notificar una brecha en un máximo de 60 días").
- **Cómo lo aborda el SGSI:** ISO/IEC 27001:2022 pide determinar cuáles de esos requisitos se abordan a través del sistema de gestión (cl. 4.2 c).

### 1.1 Partes interesadas internas

| Parte interesada | Expectativas | Requisitos | Cómo lo aborda el SGSI |
|---|---|---|---|
| **Directorio y accionistas** | Proteger la reputación y el valor de la empresa; evitar incidentes que frenen el crecimiento | Aprobar el apetito de riesgo y la política de seguridad; rendición de cuentas por cumplimiento | Reportes periódicos del CISO, revisión por la Dirección (cl. 9.3) |
| **Dirección (CEO)** | Certificar ISO 27001 en 12 meses para competir en licitaciones | Cumplir los SLA y las obligaciones contractuales con clientes | Objetivos de seguridad, plan de tratamiento de riesgos |
| **CISO y equipo de seguridad** | Recursos, apoyo de la Dirección y procesos claros para gestionar la seguridad | Mantener el SGSI, el análisis de riesgos anual (también exigido por HIPAA) y las evidencias para auditorías | Metodología de riesgos, registro de riesgos, programa de auditoría |
| **Desarrollo, QA e Infraestructura** | Controles que no frenen la entrega ágil; reglas técnicas claras | Desarrollo seguro y gestión de cambios en la página de pago (PCI DSS, requisito 6) | Política de desarrollo seguro, controles integrados al CI/CD |
| **Soporte y Comercial** | Poder resolver reclamos y vender sin trabas innecesarias | Acceso a datos de pacientes solo por necesidad; confidencialidad | Control de accesos por rol, capacitación |
| **Empleados en general** | Reglas claras, capacitación y protección de sus propios datos personales | Deber de confidencialidad (art. 10, Ley 25.326); uso aceptable de los recursos | Políticas, acuerdos de confidencialidad, programa de concientización |

### 1.2 Partes interesadas externas

| Parte interesada | Expectativas | Requisitos | Cómo lo aborda el SGSI |
|---|---|---|---|
| **Pacientes** | Que sus datos de salud y de pago no se filtren; plataforma disponible para sacar turnos | Derechos de acceso, rectificación y supresión (arts. 14 a 16, Ley 25.326); en EE.UU., derechos HIPAA | Controles de confidencialidad, procedimiento de atención de derechos |
| **Clínicas de Argentina** | Plataforma disponible y confiable; que SaludPay cuide los datos de sus pacientes | Obligaciones de encargado del tratamiento (art. 25, Ley 25.326); SLA de disponibilidad del 99,9% | Anexo contractual de tratamiento de datos, plan de continuidad |
| **Clínicas de EE.UU.** | Un socio confiable que les permita cumplir HIPAA | Cumplir el BAA; notificar brechas sin demora irrazonable y en un máximo de 60 días | Programa HIPAA, procedimiento de notificación de brechas |
| **Prepagas y grandes clientes** | Proveedor certificado con evidencia de seguridad | Certificación ISO 27001 y respuesta a cuestionarios de seguridad en licitaciones | Certificación, paquete de evidencias para clientes |
| **AAIP** (autoridad de control argentina) | Cumplimiento proactivo de la protección de datos | Ley 25.326, inscripción de bases de datos, medidas de seguridad (Res. AAIP 47/2018) | Registro de tratamientos, controles de seguridad |
| **HHS – Office for Civil Rights** (EE.UU.) | Que los *Business Associates* protejan la información de salud | HIPAA Privacy, Security y Breach Notification Rules | Análisis de riesgos HIPAA, salvaguardas, notificación de brechas |
| **Marcas de tarjeta y adquirente** | Que los datos de tarjeta no se comprometan | PCI DSS v4.0.1, con validación anual como proveedor de servicios | Tokenización, seguridad de la página de pago (requisitos 6.4.3 y 11.6.1) |
| **Proveedores críticos** (AWS, pasarela de pagos, mensajería) | Relación estable y requisitos de seguridad claros | Cumplir los contratos, BAA con AWS, modelo de responsabilidad compartida en la nube | Gestión de proveedores, evaluación de terceros |
| **Aseguradora de ciberriesgo** | Un cliente con riesgo controlado | Controles mínimos para mantener la póliza: MFA, backups y plan de respuesta | Evidencias de controles implementados |
| **Organismo certificador** | Un SGSI implementado, eficaz y con evidencias | Requisitos de ISO/IEC 27001:2022 para otorgar y mantener la certificación | Todo el SGSI: auditoría interna, revisión por la Dirección, mejora continua |

> 💡 **Observación del analista:** casi todas las expectativas externas se reducen a **confianza**, y muchos requisitos se repiten entre partes (la notificación de brechas aparece en clínicas, HHS y pacientes). Por eso un mismo control, como el procedimiento de notificación del riesgo R-08, cumple con varias partes a la vez.

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
