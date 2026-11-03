# 🗺️ Plan de trabajo del laboratorio

Hoja de ruta para construir el laboratorio fase por fase. Cada fase tiene entregables concretos, lo que vas a aprender y un criterio de "terminado". Marcá las casillas a medida que avanzás.

**Dedicación sugerida:** 6–8 horas por semana → ~10 a 12 semanas para completar todo.

---

## Fase 0 · Preparación (semana 1)

- [ ] Crear el repositorio `grc-lab-saludpay` en GitHub (público) y subir esta estructura (ver [cómo subirlo](#-cómo-subir-el-repositorio-a-github) al final)
- [ ] Actualizar el perfil de GitHub (README de perfil, bio, empresa, repos fijados)
- [ ] Instalar herramientas: Git, VS Code (con extensiones *Markdown Preview Mermaid Support* y *Rainbow CSV*), Docker Desktop o una VM Linux (Ubuntu Server)
- [ ] Leer toda la Fase 1 y ajustar lo que quieras: es *tu* empresa ficticia

## Fase 1 · Contexto y alcance (semana 1–2) ✅

Entregables ya armados en [`01-contexto/`](01-contexto/):

- [x] Descripción de la empresa y contexto interno/externo (ISO 27001 cl. 4.1)
- [x] Alcance del SGSI con exclusiones e interfaces (cl. 4.3)
- [x] Arquitectura y flujos de datos sensibles
- [x] Inventario de 30 activos con clasificación C-I-D (A.5.9, A.5.12)
- [x] Registro de tratamientos de datos personales (Ley 25.326)
- [x] Partes interesadas y matriz de requisitos legales (cl. 4.2, A.5.31)

**Tu tarea:** revisar cada documento, entender *por qué* está así y modificar lo que no te convenza. En una entrevista te van a preguntar por tus decisiones, así que tienen que ser tuyas.

## Fase 2 · Gestión de riesgos (semana 3–4)

**Aprendés:** el corazón de ISO 27001 (cl. 6.1.2 y 6.1.3, 8.2 y 8.3) y de la HIPAA Security Rule (§164.308(a)(1), análisis y gestión de riesgos).

- [ ] **Metodología de riesgos** (`02-riesgos/01-metodologia.md`): escalas de probabilidad e impacto (1–5), matriz de calor, criterios de aceptación del riesgo (apetito), dueños de riesgo. Basada en ISO 31000 / ISO 27005
- [ ] **Catálogo de amenazas y vulnerabilidades** relevante para SaludPay (ransomware, phishing, error de configuración cloud, acceso indebido de soporte, fuga por exportación CSV, *skimming* en el checkout, caída del proveedor cloud, etc.)
- [ ] **Registro de riesgos** (`02-riesgos/registro-riesgos.csv`): 20–25 riesgos vinculados a los activos del inventario, con riesgo inherente, controles existentes y riesgo residual
- [ ] **Plan de tratamiento** (`02-riesgos/03-plan-tratamiento.md`): mitigar, transferir, evitar o aceptar; responsable, fecha y control del Anexo A asociado
- [ ] **Script en Python** (`scripts/riesgos.py`) que lea el CSV y genere la matriz de calor y un resumen (riesgos por nivel, por dueño, por marco normativo). *Acá suma tu perfil técnico*
- [ ] Acta de aceptación de riesgos residuales firmada (simulada) por el dueño del riesgo

**Terminado cuando:** cada riesgo alto tiene un tratamiento con responsable y fecha, y cada activo crítico tiene al menos un riesgo evaluado.

## Fase 3 · Declaración de Aplicabilidad y políticas (semana 5–6)

**Aprendés:** el Anexo A de ISO 27001:2022 (93 controles en 4 temas: organizacionales, de personas, físicos y tecnológicos) y la redacción de políticas.

- [ ] **SoA** (`03-soa-y-politicas/soa.csv`): los 93 controles con aplicabilidad (sí/no), justificación, estado de implementación y vínculo con los riesgos de la Fase 2
- [ ] **Política de Seguridad de la Información** (la "política madre", aprobada por la Dirección)
- [ ] Política de Control de Accesos
- [ ] Política de Clasificación y Manejo de la Información
- [ ] Política de Protección de Datos Personales (Ley 25.326 + HIPAA)
- [ ] Política de Gestión de Incidentes (incluye plazos de notificación: 60 días HIPAA, comunicación a clínicas)
- [ ] Política de Gestión de Proveedores
- [ ] Política de Respaldo y Recuperación
- [ ] Política de Desarrollo Seguro (aprovechá tu experiencia en QA)
- [ ] Plantilla común de documento (control de versiones, aprobación, fecha de revisión)

**Terminado cuando:** cada control excluido tiene una justificación y cada política referencia los controles que implementa.

## Fase 4 · Mapeo multinorma (semana 7)

**Aprendés:** a trabajar con varios marcos sin duplicar esfuerzo, que es lo que más se valora en GRC.

- [ ] **Matriz de controles** (`04-mapeo-normativo/matriz.csv`): cada fila es un control de SaludPay (ej.: "MFA para accesos remotos y privilegiados") con sus equivalencias en ISO 27001 (Anexo A), PCI DSS (requisitos 1–12), HIPAA Security Rule (§164.308/310/312) y Ley 25.326 / Res. AAIP 47/2018
- [ ] **Gap analysis** por marco: porcentaje de cumplimiento y brechas principales
- [ ] Gráfico de cumplimiento por marco (generado con un script)
- [ ] Documento breve: "Cómo un mismo control satisface cuatro marcos" (excelente para mostrar en entrevistas)

## Fase 5 · Evidencias técnicas (semana 8–9)

**Aprendés:** cómo se prueba que un control funciona, y *compliance as code*.

- [ ] Levantar un servidor Ubuntu (VM o Docker) que represente un servidor de SaludPay
- [ ] Implementar y evidenciar 6–8 controles: política de contraseñas, bloqueo por intentos fallidos, SSH solo con clave, firewall (ufw), registro de auditoría (auditd), backups automáticos con prueba de restauración, actualizaciones automáticas, cifrado de un volumen
- [ ] **Script de verificación** (`scripts/check_controles.sh` o `.py`) que revise esos controles y genere un reporte de cumplimiento (OK / NO OK) con el control ISO y PCI asociado
- [ ] Opcional: correr **Lynis** u **OpenSCAP** y analizar el resultado contra la SoA
- [ ] Opcional (con tu formación AWS): revisar una cuenta free tier con AWS Config / Security Hub y documentar hallazgos
- [ ] Carpeta de evidencias organizada por control (capturas, salidas de comandos, configuraciones)

> ⚠️ Nunca subas contraseñas, claves ni datos reales al repositorio. Usá datos ficticios y revisá antes de cada `git push`.

## Fase 6 · Auditoría interna (semana 10–11)

**Aprendés:** ISO 27001 cl. 9.2 y 10.2, e ISO 19011 (directrices de auditoría). **Coincide con tu curso de Auditor Interno**: aplicá ahí lo que vayas aprendiendo.

- [ ] Programa anual de auditoría interna
- [ ] Plan de auditoría (alcance, criterios, agenda, auditados)
- [ ] Checklist de auditoría (cláusulas 4 a 10 + muestra de controles del Anexo A)
- [ ] Simulación de entrevistas y revisión de evidencias (podés usar las evidencias de la Fase 5 e "inventar" algunas fallas a propósito)
- [ ] **Informe de auditoría** con hallazgos: no conformidades mayores/menores, observaciones y oportunidades de mejora
- [ ] Cada no conformidad cargada como **Issue** en GitHub con etiqueta, responsable, análisis de causa raíz y acción correctiva
- [ ] Revisión por la Dirección (cl. 9.3): acta simulada

## Fase 7 · Continuidad del negocio (semana 12)

**Aprendés:** ISO 22301 y la relación con la disponibilidad del SGSI (A.5.29, A.5.30).

- [ ] Análisis de impacto en el negocio (BIA): procesos críticos, RTO y RPO
- [ ] Estrategias de continuidad (multi-región, proveedores alternativos)
- [ ] Plan de continuidad para el escenario "ransomware en producción"
- [ ] Ejercicio de mesa (*tabletop*) simulado con su informe de lecciones aprendidas

## Fase 8 · Cierre y difusión

- [ ] Completar el README del repo con los resultados de cada fase
- [ ] Publicar un post en LinkedIn contando el proyecto y lo aprendido
- [ ] Agregar el proyecto al CV en una sección "Proyectos" (redacción sugerida abajo)
- [ ] Preparar un "pitch" de 2 minutos para entrevistas: el caso, tres hallazgos interesantes y qué harías distinto

---

## 📄 Redacción sugerida para el CV

> **Proyecto práctico — Laboratorio GRC "SaludPay"** · [github.com/PabloSammartino/grc-lab-saludpay](https://github.com/PabloSammartino/grc-lab-saludpay)
> Implementación simulada de un SGSI ISO/IEC 27001:2022 para una empresa SaaS ficticia del sector salud y pagos, con alcance multinorma (Ley 25.326, HIPAA y PCI DSS v4.0.1).
> - Definición de alcance, inventario y clasificación de 30 activos, registro de tratamientos de datos personales y matriz de requisitos legales.
> - Análisis y tratamiento de riesgos (ISO 31000 / 27005), Declaración de Aplicabilidad y set de políticas.
> - Mapeo de controles entre cuatro marcos y verificación técnica automatizada de controles en Linux.
> - Auditoría interna simulada con gestión de no conformidades.

*(Ajustalo a medida que completes fases: solo poné lo que efectivamente hiciste.)*

---

## 🚀 Cómo subir el repositorio a GitHub

1. Entrá a GitHub → **New repository** → nombre `grc-lab-saludpay`, **Public**, sin README (ya tenés uno) → **Create repository**.
2. Descomprimí el `.zip` en tu computadora y abrí una terminal en la carpeta `grc-lab-saludpay`.
3. Ejecutá:

```bash
git init
git add .
git commit -m "Fase 1: contexto y alcance del SGSI de SaludPay"
git branch -M main
git remote add origin https://github.com/PabloSammartino/grc-lab-saludpay.git
git push -u origin main
```

4. En el repositorio, en **About** (engranaje a la derecha), agregá una descripción y *topics*: `grc`, `iso27001`, `pci-dss`, `hipaa`, `data-protection`, `information-security`, `compliance`.
5. Hacé un commit por cada entregable o fase, con mensajes claros. Un historial de commits ordenado también muestra método de trabajo.
