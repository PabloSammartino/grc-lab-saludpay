# 05 · Registro de tratamientos de datos personales

> **Referencia normativa:** Ley 25.326 de Protección de los Datos Personales y su Decreto Reglamentario 1558/2001; Resolución AAIP 47/2018 (medidas de seguridad recomendadas). Complementa el control 5.34 de ISO/IEC 27001:2022 (privacidad y protección de datos personales).
>
> **Nota:** la Ley 25.326 no exige expresamente un "registro de actividades de tratamiento" como el RGPD europeo, pero sí exige **inscribir las bases de datos** ante la autoridad de control (art. 21). Este registro interno es una buena práctica que facilita esa inscripción, la atención de derechos y la demostración de cumplimiento.

## 1. Rol de SaludPay frente a cada tratamiento

Este es el punto jurídico más importante del documento, porque define qué obligaciones tiene SaludPay:

- **Responsable del tratamiento** (art. 2): quien decide sobre la finalidad y el uso de los datos.
- **Encargado del tratamiento / prestador de servicios informatizados** (art. 25): quien trata datos **por cuenta de** otro. No puede usarlos para una finalidad distinta a la del contrato ni cederlos, y al terminar la relación debe destruirlos (salvo autorización expresa para conservarlos con fines de un nuevo servicio).

| Tratamiento | Rol de SaludPay | Responsable |
|---|---|---|
| Datos de pacientes en la plataforma | Encargado | Cada clínica cliente |
| Datos de empleados | Responsable | SaludPay |
| Contactos comerciales de clínicas | Responsable | SaludPay |
| Usuarios del sitio web (formularios, cookies) | Responsable | SaludPay |

## 2. Registro

| ID | Tratamiento | Finalidad | Categorías de titulares | Categorías de datos | ¿Datos sensibles? | Base legal (Ley 25.326) | Destinatarios / cesiones | Transferencia internacional | Plazo de conservación | Sistema |
|---|---|---|---|---|---|---|---|---|---|---|
| T-01 | Gestión de turnos | Reserva, reprogramación y cancelación de turnos por cuenta de la clínica | Pacientes | Identificatorios, contacto, fecha de nacimiento, cobertura médica, especialidad, motivo de consulta | **Sí — salud** (art. 2 y 7) | Lo determina el responsable (clínica). Datos de salud: art. 8, tratamiento por establecimientos sanitarios y profesionales, respetando el secreto profesional | Clínica responsable, proveedores de mensajería (subencargados) | **Sí** — Brasil (AWS sa-east-1) y logs en EE.UU. | Mientras dure el contrato con la clínica; luego devolución y destrucción (art. 25) | A-001, A-006, A-007 |
| T-02 | Cobro de consultas | Procesar pagos de pacientes por cuenta de la clínica | Pacientes | Nombre, monto, token de pago, últimos 4 dígitos | No | Contrato con la clínica / ejecución de la relación con el paciente | Pasarela de pagos | Según pasarela | 10 años (obligaciones contables y fiscales del responsable, a confirmar por la clínica) | A-004 |
| T-03 | Recordatorios | Enviar recordatorios de turnos | Pacientes | Nombre, teléfono, email, fecha y hora del turno, nombre de la clínica | No (minimizado: sin especialidad ni motivo) | Por cuenta de la clínica | Proveedores de email, SMS, WhatsApp | **Sí** — EE.UU. (proveedores de mensajería) | 12 meses | A-003 |
| T-04 | Soporte a clínicas | Resolver reclamos e incidentes | Personal de clínicas, pacientes | Contacto, datos del turno o pago involucrado | Eventualmente | Contrato | — | No | 24 meses desde el cierre del caso | A-103 |
| T-05 | Gestión de RRHH | Administración de personal y liquidación de sueldos | Empleados y postulantes | Identificatorios, domicilio, datos bancarios, CUIL, certificados médicos | **Sí** — certificados médicos | Relación laboral; obligaciones legales (art. 5 inc. 2) | Organismos de seguridad social, ART, banco | Según proveedor de RRHH | 10 años desde el egreso (plazos de prescripción laboral y previsional — a validar con Legales) | A-010 |
| T-06 | Gestión comercial | Contactar y gestionar clínicas clientes y prospectos | Contactos de clínicas | Nombre, cargo, email, teléfono | No | Relación contractual o precontractual; consentimiento para marketing | CRM (proveedor) | **Sí** — EE.UU. | Mientras dure la relación + 24 meses | CRM |
| T-07 | Sitio web | Formularios de contacto y analítica | Visitantes | Nombre, email, IP, cookies | No | Consentimiento (art. 5) | Proveedor de analítica | **Sí** — EE.UU. | 13 meses | Sitio web |

## 3. Requisitos de cumplimiento derivados

| # | Requisito | Artículo | Estado inicial | Acción |
|---|---|---|---|---|
| R-01 | Inscribir las bases de datos de las que SaludPay es responsable (T-05, T-06, T-07) en el Registro Nacional de Bases de Datos | Art. 21 | ❓ Sin evidencia | Verificar inscripción y actualizarla |
| R-02 | Contratos con clínicas que regulen el rol de encargado: finalidad, seguridad, confidencialidad, destino de los datos al terminar | Art. 25 | ⚠️ Contrato estándar sin cláusula específica | Redactar anexo de tratamiento de datos |
| R-03 | Contratos con subencargados (mensajería, cloud) con obligaciones equivalentes | Art. 25 y 9 | ⚠️ Parcial | Revisar contratos de proveedores |
| R-04 | Mecanismo legal para transferencias a países sin protección adecuada (Brasil, EE.UU.) | Art. 12 | ❌ No documentado | Evaluar cláusulas contractuales modelo de la autoridad o consentimiento; revisar si conviene dejar de enviar datos personales a los logs |
| R-05 | Medidas de seguridad técnicas y organizativas | Art. 9; Res. AAIP 47/2018 | ⚠️ Parcial | Se cubre con el SGSI ISO 27001 |
| R-06 | Deber de confidencialidad del personal | Art. 10 | ⚠️ Acuerdo de confidencialidad genérico | Incluir cláusula específica de datos personales y de salud |
| R-07 | Procedimiento para atender derechos de acceso, rectificación, actualización y supresión (y derivarlos a la clínica cuando SaludPay es encargado) | Art. 14 a 16 | ❌ No existe | Redactar procedimiento y plazos (10 días corridos para acceso; 5 días hábiles para rectificación/supresión) |
| R-08 | Información al titular al recabar datos (finalidad, destinatarios, derechos, responsable) | Art. 6 | ⚠️ Política de privacidad desactualizada | Actualizar política de privacidad del sitio y de la app |
| R-09 | Gestión y registro de incidentes de seguridad que afecten datos personales | Res. AAIP 47/2018 | ⚠️ Procedimiento general de incidentes sin componente de privacidad | Incorporar evaluación de impacto en titulares y comunicación a clínicas |

> 💡 **Nota de aprendizaje:** acá es donde tu formación de abogado marca diferencia. Un perfil puramente técnico suele pasar por alto la distinción responsable/encargado, que cambia por completo las obligaciones de la empresa y lo que hay que exigir en los contratos.
>
> ⚠️ **Vigencia normativa:** la Ley 25.326 sigue plenamente vigente, aunque hay proyectos de reforma integral en el Congreso. Si se aprueba una nueva ley, este registro deberá actualizarse.
