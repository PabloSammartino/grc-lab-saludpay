# 02 · Alcance del SGSI

> **Referencia normativa:** ISO/IEC 27001:2022, cláusula 4.3 (determinación del alcance del SGSI).
> **Versión:** 1.0 · **Estado:** Borrador para aprobación del CISO · **Elaborado por:** Analista GRC

## 1. Declaración de alcance

> El Sistema de Gestión de Seguridad de la Información (SGSI) de SaludPay S.A. comprende **el diseño, desarrollo, operación y soporte de la plataforma SaaS de gestión de turnos y cobros para prestadores de salud**, incluyendo la infraestructura cloud que la soporta, los procesos de desarrollo y despliegue, la atención al cliente y la gestión de proveedores críticos, llevados a cabo desde la sede de Ciudad Autónoma de Buenos Aires y por personal en modalidad remota.

## 2. Qué queda dentro del alcance

| Categoría | Elementos incluidos |
|---|---|
| Procesos | Desarrollo de software (incluye QA), operación y monitoreo de la plataforma, gestión de cambios, soporte al cliente, alta/baja de clientes, gestión de accesos, gestión de incidentes, gestión de proveedores, RRHH (en lo relativo a seguridad: ingreso, capacitación, egreso) |
| Sistemas | Aplicación web, app móvil, API pública, bases de datos de producción, entornos de staging, pipeline CI/CD, herramientas de monitoreo y logging |
| Infraestructura | Cuenta de producción de AWS (us-east-1 y sa-east-1), cuentas de staging, VPN corporativa, notebooks de empleados |
| Información | Datos de pacientes, datos de clínicas clientes, datos de transacciones (tokens de pago, no números de tarjeta), código fuente, credenciales y secretos, información de empleados |
| Ubicaciones | Oficina en CABA, trabajo remoto en Argentina y EE.UU. |
| Personas | Todo el personal, contratistas con acceso a sistemas |

## 3. Exclusiones y justificación

| Exclusión | Justificación |
|---|---|
| Datos completos de tarjeta (PAN, CVV) | No ingresan a los sistemas de SaludPay: el paciente los carga en un formulario embebido (iframe) del proveedor de pagos certificado PCI DSS, que devuelve un *token*. El **alcance PCI** se trata en la sección 5. |
| Data center físico | No hay infraestructura propia; la seguridad física del centro de datos es responsabilidad de AWS (modelo de responsabilidad compartida). Se gestiona como **proveedor** (control de terceros). |
| Sistemas de las clínicas clientes | Son responsabilidad de cada cliente. SaludPay solo responde por la plataforma que provee. |
| Contabilidad general (ERP) | Sistema SaaS de terceros sin datos de pacientes; riesgo bajo. Se revisará su inclusión en el segundo año. |

## 4. Interfaces y dependencias

La información entra y sale del alcance a través de estas interfaces, que deben quedar controladas:

| Interfaz | Dirección | Contraparte | Control esperado |
|---|---|---|---|
| Pasarela de pagos (iframe + API) | Entrada/salida | Proveedor de pagos (PCI DSS Nivel 1) | Integración por token, AOC (*Attestation of Compliance*) vigente del proveedor |
| Integraciones con sistemas de las clínicas (API) | Entrada/salida | Clínicas clientes | Autenticación OAuth 2.0, TLS 1.2+ |
| Mensajería (email, SMS, WhatsApp) | Salida | Proveedores de comunicaciones | Contrato con cláusulas de confidencialidad, minimización de datos en mensajes |
| Proveedor cloud | Infraestructura | AWS | Reportes SOC 2 / ISO 27001 del proveedor, BAA de AWS para datos de EE.UU. |
| Herramientas SaaS internas | Interna | Google Workspace, Jira, Slack, GitHub | SSO con MFA, revisión anual de proveedores |

## 5. Alcance por marco normativo

Cada marco tiene su propia lógica de alcance. Esta tabla evita confusiones durante las auditorías:

| Marco | Alcance específico | Rol de SaludPay |
|---|---|---|
| **ISO/IEC 27001:2022** | Todo lo descripto en la sección 2 | Organización que implementa el SGSI |
| **Ley 25.326** | Todo tratamiento de datos personales de personas en Argentina | **Encargado de tratamiento** respecto de los datos de pacientes (el responsable es cada clínica, art. 25) y **responsable** respecto de sus propios empleados, contactos comerciales y usuarios de la web |
| **HIPAA** | Información de salud protegida electrónica (ePHI) de pacientes de las 18 clínicas de EE.UU. | **Business Associate** de cada clínica (*covered entity*), con un BAA firmado |
| **PCI DSS v4.0.1** | Componentes que pueden afectar la seguridad de los datos de tarjeta: la página de checkout que aloja el iframe, los scripts que se cargan en ella, la integración con la pasarela | **Proveedor de servicios** con alcance reducido por tokenización. Al ser proveedor de servicios, valida con el **SAQ D para proveedores de servicios** |
| **ISO 22301** | Procesos críticos: reserva de turnos y cobro | Fase posterior del laboratorio |

## 6. Aprobación

| Rol | Nombre | Firma | Fecha |
|---|---|---|---|
| Elaboró | Analista GRC | — | — |
| Revisó | CISO | — | — |
| Aprobó | CEO | — | — |

> 💡 **Nota de aprendizaje:** un alcance mal definido es uno de los hallazgos más frecuentes en auditorías de certificación. Las exclusiones siempre tienen que estar justificadas, y las interfaces con terceros deben estar identificadas aunque estén "fuera".
