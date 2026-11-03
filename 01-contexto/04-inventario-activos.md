# 04 · Inventario de activos de información

> **Referencia normativa:** ISO/IEC 27001:2022, Anexo A, control 5.9 (inventario de información y otros activos asociados) y 5.12 (clasificación de la información). PCI DSS v4.0.1, requisito 12.5.1 (inventario de componentes en alcance).

El inventario completo está en [`04-inventario-activos.csv`](04-inventario-activos.csv) (30 activos). Se mantiene en CSV para que pueda abrirse en Excel / Google Sheets y procesarse con scripts en las fases siguientes.

## 1. Columnas del inventario

| Columna | Significado |
|---|---|
| `id` | Identificador único. Prefijos: **A-0xx** información, **A-1xx** software, **A-2xx** infraestructura, **A-3xx** proveedores, **A-4xx** personas |
| `dueno` | Responsable del activo (quien decide sobre su protección, no necesariamente quien lo opera) |
| `clasificacion` | Nivel según el esquema de la sección 2 |
| `confidencialidad` / `integridad` / `disponibilidad` | Valoración de 1 (bajo) a 3 (alto) |
| `criticidad` | El valor más alto de C-I-D (criterio conservador) |
| `datos_personales` / `datos_salud` | Relevante para Ley 25.326 |
| `ePHI_HIPAA` | Contiene o procesa información de salud protegida electrónica de pacientes de EE.UU. |
| `alcance_PCI` | **Sí**: componente del entorno de pago; **Conectado**: puede afectar su seguridad; **No**: fuera de alcance |

## 2. Esquema de clasificación de la información

| Nivel | Definición | Ejemplos | Manejo mínimo |
|---|---|---|---|
| **Público** | Información aprobada para difusión | Sitio web, folletos | Sin restricciones |
| **Interno** | Uso interno; su divulgación tendría impacto bajo | Procedimientos, organigrama | Solo personal de SaludPay |
| **Confidencial** | Su divulgación causaría daño al negocio o a terceros | Contratos, código fuente, datos de clínicas | Acceso por necesidad de saber, cifrado en tránsito |
| **Confidencial - Sensible** | Datos de salud o datos personales sensibles | Motivo de consulta, especialidad, cobertura | Cifrado en reposo y tránsito, registro de accesos, minimización |
| **Restringido** | Acceso solo para roles específicos y nominados | Secretos, credenciales de producción | Acceso privilegiado con MFA, rotación, gestor de secretos |

## 3. Escala de valoración C-I-D

| Valor | Confidencialidad | Integridad | Disponibilidad |
|---|---|---|---|
| **1 - Bajo** | La divulgación no genera daño relevante | Un error se corrige sin impacto | Puede no estar disponible más de 3 días |
| **2 - Medio** | Daño acotado, sin consecuencias legales | Afecta procesos internos | Tolera hasta 24 horas de caída |
| **3 - Alto** | Daño a pacientes, sanciones legales o pérdida de clientes | Afecta pagos, turnos o decisiones de salud | No tolera más de 4 horas de caída |

## 4. Observaciones del analista

1. **9 de los 11 activos de información contienen datos personales** y cerca de la mitad contiene (o puede contener) datos de salud. La protección de datos personales es el eje del programa, no un anexo.
2. **Los logs (A-006) pueden contener datos sensibles** sin que nadie lo haya decidido. Es un riesgo típico: los desarrolladores registran el contenido de los requests para depurar.
3. **El alcance PCI es reducido pero existe.** La página de checkout (A-101) y el WAF (A-205) están en alcance aunque SaludPay nunca vea un número de tarjeta.
4. **Las personas también son activos.** El equipo de soporte (A-403) tiene acceso amplio a datos de pacientes: hay que medir ese riesgo.
5. **Los proveedores críticos (A-3xx)** necesitan evaluación de riesgo de terceros, contratos con cláusulas de seguridad y, en el caso de los que tocan ePHI, un BAA.

> 💡 **Nota de aprendizaje:** en una empresa real este inventario se arma con entrevistas a los dueños de cada área y con herramientas de descubrimiento (por ejemplo, el inventario de recursos de la consola cloud). El inventario nunca está "terminado": se revisa al menos una vez al año y ante cada cambio significativo.
