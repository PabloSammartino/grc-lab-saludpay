# 🛡️ GRC Lab — SaludPay S.A.

**Laboratorio práctico de Gobierno, Riesgo y Cumplimiento (GRC)** en el que implemento, sobre una empresa ficticia, el trabajo que realiza un analista GRC: definición del alcance, inventario de activos, análisis de riesgos, políticas, Declaración de Aplicabilidad, mapeo entre normas, evidencias técnicas y auditoría interna.

> ⚠️ **SaludPay S.A. es una empresa ficticia.** Todos los datos, personas y sistemas de este repositorio son inventados con fines de aprendizaje.

---

## 🏥 El caso

**SaludPay** es una empresa argentina que ofrece una plataforma SaaS de **turnos y cobros online para clínicas**, con clientes en Argentina y en EE.UU. Su modelo de negocio la expone a cuatro marcos a la vez:

| Marco | Por qué aplica |
|---|---|
| **ISO/IEC 27001:2022** | El Directorio decidió certificar para competir en licitaciones |
| **Ley 25.326** (Argentina) | Trata datos personales y datos de salud de pacientes argentinos |
| **HIPAA** (EE.UU.) | Es *Business Associate* de 18 clínicas estadounidenses |
| **PCI DSS v4.0.1** | Procesa cobros con tarjeta como proveedor de servicios |

📄 Detalle completo: [01-contexto/01-descripcion-empresa.md](01-contexto/01-descripcion-empresa.md)

---

## 🗂️ Estructura y avance

| Fase | Contenido | Estado |
|---|---|---|
| [01 · Contexto y alcance](01-contexto/) | Empresa, alcance del SGSI, arquitectura y flujos de datos, inventario de activos, registro de tratamientos de datos, partes interesadas, matriz legal y análisis FODA | ✅ Completa |
| [02 · Gestión de riesgos](02-riesgos/) | Metodología, registro de 8 riesgos evaluados, plan de tratamiento | 🚧 En curso |
| [03 · SoA y políticas](03-soa-y-politicas/) | Declaración de Aplicabilidad (93 controles del Anexo A) y políticas clave | 🔲 Pendiente |
| [04 · Mapeo normativo](04-mapeo-normativo/) | Matriz ISO 27001 ↔ PCI DSS ↔ HIPAA ↔ Ley 25.326 | 🔲 Pendiente |
| [05 · Evidencias técnicas](05-evidencias-tecnicas/) | Laboratorio Linux/Docker, controles implementados y scripts de verificación | 🔲 Pendiente |
| [06 · Auditoría interna](06-auditoria-interna/) | Programa, checklist, informe y no conformidades | 🔲 Pendiente |
| [07 · Continuidad del negocio](07-continuidad/) | BIA y plan de continuidad (ISO 22301) | 🔲 Pendiente |

Las no conformidades y acciones correctivas se gestionan como **Issues** de este repositorio, simulando la herramienta de ticketing del área.

---

## 🧭 Hallazgos destacados hasta ahora

- **Transferencia internacional sin respaldo documentado:** los logs de la plataforma argentina se envían a EE.UU. y pueden contener datos personales (art. 12, Ley 25.326).
- **Rol de encargado mal reflejado en los contratos:** SaludPay trata los datos de pacientes por cuenta de las clínicas, pero el contrato estándar no lo regula (art. 25, Ley 25.326).
- **Alcance PCI reducido pero no nulo:** aunque los datos de tarjeta van directo a la pasarela, la página de checkout que aloja el formulario de pago está en alcance (PCI DSS 6.4.3 y 11.6.1).

---

## 📚 Marcos de referencia

ISO/IEC 27001:2022 · ISO/IEC 27002:2022 · ISO 31000 · ISO 22301 · Ley 25.326 y Res. AAIP 47/2018 · HIPAA (45 CFR Partes 160 y 164) · PCI DSS v4.0.1

> Los textos de las normas ISO están protegidos por derechos de autor. Este repositorio solo cita números de cláusulas y controles y describe su contenido con palabras propias.

---

## 👤 Autor

**Pablo Sammartino** — Abogado orientado a GRC y Seguridad de la Información.
Estudiante de la Tecnicatura Universitaria en Ciberseguridad (UGR) · Auditor Interno ISO/IEC 27001 (en curso).

[LinkedIn](https://www.linkedin.com/in/psammartino/)
