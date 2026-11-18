# ✍️ Evaluación de riesgos R-01 a R-08

Razonamiento detrás de cada evaluación del [registro de riesgos](registro-riesgos.csv), aplicando la [metodología](01-metodologia.md). **R-01 y R-02** se resolvieron primero como **modelos de referencia**; **R-03 a R-08** se evaluaron como ejercicio a partir de esos modelos. Para cada riesgo se conserva la justificación de los números y la principal lección que dejó.

**Estado:** ✅ Completo. Los resultados están cargados en el [registro de riesgos](registro-riesgos.csv).

## Resumen

| Riesgo | Inherente | Residual | Tratamiento | Lección clave |
|---|---|---|---|---|
| R-01 · Ransomware *(modelo)* | 🟥 20 | 🟥 15 | Mitigar | Un control mal diseñado (backups en la misma cuenta) no protege |
| R-02 · Logs enviados a EE.UU. *(modelo)* | 🟧 12 | 🟧 12 | Mitigar | Un riesgo de cumplimiento es tan riesgo como un ataque |
| R-03 · Soporte que consulta fichas | 🟥 16 | 🟥 16 | Mitigar | Un control que no apunta a la amenaza no baja el riesgo |
| R-04 · Skimming en el checkout | 🟥 16 | 🟥 16 | Mitigar + evitar | Ataque a la cadena de suministro; prevenir + detectar |
| R-05 · Exportación CSV | 🟥 20 | 🟥 16 | Mitigar | Responsable (clínica) vs. encargado (SaludPay) |
| R-06 · Caída de AWS | 🟧 10 | 🟨 8 | Mitigar | Tratamiento proporcional al riesgo |
| R-07 · Phishing | 🟥 20 | 🟥 16 | Mitigar | Controles que apuntan pero son débiles |
| R-08 · Notificación tardía | 🟥 16 | 🟧 12 | Mitigar | Separar el hecho del riesgo; lo legal se trata siempre |

## Modelos de referencia

### R-01 · Ransomware en la base de pacientes

| | Probabilidad | Impacto | Riesgo | Nivel |
|---|---|---|---|---|
| Inherente | 4 | 5 | 20 | 🟥 Crítico |
| Residual | 3 | 5 | 15 | 🟥 Crítico |

- **Justificación:** el sector salud es de los más atacados por ransomware y SaludPay tiene claves de AWS sin MFA. El impacto es catastrófico: plataforma inoperativa varios días y posible exposición de datos de salud de más de 10.000 personas.
- **Residual:** el MFA en la consola web y las alertas bajan algo la probabilidad. El impacto no baja: los backups están en la misma cuenta AWS que el atacante podría comprometer, y la restauración nunca se probó.
- **Tratamiento:** mitigar.
- **Acciones:** backups inmutables en una cuenta separada, MFA y credenciales temporales para todo acceso privilegiado, prueba de restauración trimestral y plan de respuesta a ransomware.
- **Lección:** tener un control no alcanza si está mal diseñado. Un backup que el atacante puede borrar no protege contra el ransomware.

---

### R-02 · Logs con datos personales enviados a EE.UU.

| | Probabilidad | Impacto | Riesgo | Nivel |
|---|---|---|---|---|
| Inherente | 3 | 4 | 12 | 🟧 Alto |
| Residual | 3 | 4 | 12 | 🟧 Alto |

- **Justificación:** los logs de la plataforma argentina guardan nombre, DNI y motivo de consulta y se envían a EE.UU. sin un mecanismo legal que ampare la transferencia (art. 12, Ley 25.326). Una denuncia ante la AAIP podría derivar en una sanción y en la pérdida de clientes.
- **Residual:** no hay ningún control que mitigue este riesgo, así que es igual al inherente.
- **Tratamiento:** mitigar (obligatorio por tratarse de un incumplimiento legal).
- **Acciones:** enmascarar o eliminar los datos personales de los logs, moverlos a la región sa-east-1 y, mientras tanto, firmar cláusulas contractuales modelo con el proveedor.
- **Lección:** en GRC, un riesgo de cumplimiento normativo es tan riesgo como un ataque informático, y se evalúa con la misma metodología.

---

## Ejercicio: R-03 a R-08

### R-03 · Soporte que consulta fichas sin justificación

| | Probabilidad | Impacto | Riesgo | Nivel |
|---|---|---|---|---|
| Inherente | 4 | 4 | 16 | 🟥 Crítico |
| Residual | 4 | 4 | 16 | 🟥 Crítico |

- **Justificación:** 15 personas con acceso sin límites a más de un millón de pacientes; el "chusmeo" de fichas es de los incidentes más comunes en salud. Impacto reputacional 4 si la ficha es de una persona conocida y llega a los medios.
- **Residual:** la VPN con MFA no frena a quien ya está adentro con acceso legítimo, y el acuerdo de confidencialidad genérico disuade poco porque no se registra qué fichas se consultan.
- **Tratamiento:** mitigar.
- **Acciones:** acceso solo a fichas con reclamo abierto, registro de consultas con revisión mensual, ocultar el motivo de consulta a soporte, cláusula de confidencialidad específica y capacitación.
- **Lección:** un control que existe pero no apunta a esta amenaza no reduce el riesgo.

---

### R-04 · Skimming en la página de checkout

| | Probabilidad | Impacto | Riesgo | Nivel |
|---|---|---|---|---|
| Inherente | 4 | 4 | 16 | 🟥 Crítico |
| Residual | 4 | 4 | 16 | 🟥 Crítico |

- **Justificación:** nueve scripts de terceros sin control en la página de pago; los ataques tipo Magecart son muy frecuentes. El impacto no viene de datos de salud (se roban datos de tarjeta), sino de lo financiero (fraude, investigación forense, multas), lo reputacional y el riesgo de perder la capacidad de procesar tarjetas.
- **Residual:** el WAF protege los servidores de SaludPay, pero el script malicioso viaja del proveedor directo al navegador del paciente. La CSP parcial no restringe scripts.
- **Tratamiento:** mitigar + evitar (parcial).
- **Acciones:** quitar los scripts no imprescindibles, inventario y autorización de los restantes (PCI DSS 6.4.3), detección de cambios en la página (PCI DSS 11.6.1) y gestión de los proveedores de scripts.
- **Lección:** cuando el atacante entra a través de un proveedor es un ataque a la cadena de suministro; conviene combinar un control preventivo con uno de detección.

---

### R-05 · Fuga por exportación CSV

| | Probabilidad | Impacto | Riesgo | Nivel |
|---|---|---|---|---|
| Inherente | 5 | 4 | 20 | 🟥 Crítico |
| Residual | 4 | 4 | 16 | 🟥 Crítico |

- **Justificación:** con más de 1.300 clientes, que alguien maneje mal una exportación varias veces por año es realista. El archivo contiene datos de salud (motivo de consulta) de cientos o miles de pacientes.
- **Residual:** que solo el administrador pueda exportar baja un poco la probabilidad, pero en los consultorios chicos la secretaria suele ser la administradora. No baja el impacto.
- **Tratamiento:** mitigar. Eliminar la exportación no es viable: las clínicas la necesitan y, como responsables, deciden sobre sus datos.
- **Acciones:** roles granulares, exportación sin motivo de consulta por defecto, registro de cada exportación, alerta ante exportaciones masivas y cláusula contractual.
- **Lección:** la clínica es la **responsable** de los datos y SaludPay la **encargada** (arts. 2 y 25, Ley 25.326). Aun así, SaludPay tiene un deber de seguridad (art. 9) y, sin registros, no puede demostrar quién exportó.

---

### R-06 · Caída de la región de AWS

| | Probabilidad | Impacto | Riesgo | Nivel |
|---|---|---|---|---|
| Inherente | 2 | 5 | 10 | 🟧 Alto |
| Residual | 2 | 4 | 8 | 🟨 Medio |

- **Justificación:** las caídas de una región entera son poco frecuentes. Sin backups, además de la caída se podrían perder datos (impacto 5).
- **Residual:** los backups en otra región evitan la pérdida de datos (el impacto baja a 4), pero sin un plan probado reconstruir lleva días. Las zonas de disponibilidad no protegen ante la caída de la región completa.
- **Tratamiento:** mitigar de forma proporcional.
- **Acciones:** plan de recuperación documentado, RTO y RPO definidos, región secundaria preparada en frío y prueba anual.
- **Lección:** la inversión tiene que ser proporcional al riesgo. Duplicar toda la infraestructura costaría casi el doble para un riesgo medio.

---

### R-07 · Phishing con robo de credenciales

| | Probabilidad | Impacto | Riesgo | Nivel |
|---|---|---|---|---|
| Inherente | 5 | 4 | 20 | 🟥 Crítico |
| Residual | 4 | 4 | 16 | 🟥 Crítico |

- **Justificación:** el phishing es el ataque más frecuente. El impacto no viene de datos de salud (un comercial no los tiene), sino de lo que el atacante puede hacer con el correo: engañar a otros empleados o enviar facturas falsas a las clínicas.
- **Residual:** el antispam frena el phishing masivo y el MFA por SMS frena las contraseñas filtradas, pero ninguno frena una página falsa que pide el código en tiempo real.
- **Tratamiento:** mitigar.
- **Acciones:** MFA resistente al phishing (FIDO2 o passkeys), capacitación trimestral con simulaciones, botón para reportar correos sospechosos y alertas de inicios de sesión inusuales.
- **Lección:** la capacitación es necesaria pero no suficiente. El mejor control es el que protege aunque la persona se equivoque.

---

### R-08 · Notificación tardía de una brecha HIPAA

| | Probabilidad | Impacto | Riesgo | Nivel |
|---|---|---|---|---|
| Inherente | 4 | 4 | 16 | 🟥 Crítico |
| Residual | 3 | 4 | 12 | 🟧 Alto |

- **Justificación:** sin procedimiento, ante una brecha nadie sabe que hay un plazo, quién decide ni a quién avisar. El impacto viene de las sanciones del HHS por la demora, del incumplimiento del BAA (las 18 clínicas de EE.UU. podrían rescindir) y del daño a pacientes que no pudieron protegerse a tiempo.
- **Residual:** el procedimiento general y el Slack de guardia aseguran que el incidente se atienda, pero no que se evalúe si es notificable ni que se avise dentro del plazo.
- **Tratamiento:** mitigar, obligatorio por la regla especial de la sección 7: un incumplimiento legal se trata siempre.
- **Acciones:** procedimiento con plazos HIPAA y de cada BAA, criterio para decidir si una brecha es notificable, registro de contactos de las clínicas, plantilla de notificación y simulacro anual.
- **Lección:** hay que separar el **hecho** (la brecha, ya evaluada en otros riesgos) del **riesgo** que se evalúa (incumplir la obligación de notificar).
