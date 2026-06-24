# Mapa de navegación de la maqueta

> Documento de **auditoría y documentación de navegación**. No modifica la maqueta ni
> agrega lógica funcional. Su único objetivo es mapear, desde `index.html`, todos los
> flujos navegables, detectar problemas y proponer correcciones para una segunda fase.
>
> **Nodo raíz analizado:** `main-files/roksyn/index.html`
>
> **Nota sobre la ruta del index:** el enunciado pide partir de `index.html`. En el
> repositorio existen dos archivos con ese nombre:
> - `main-files/roksyn/index.html` → **es el index real de la maqueta** (Home, perfil de
>   Gerencia Admon&Fin.Mkt, plantilla Roksyn / Bootstrap 5). **Este es el nodo raíz usado.**
> - `main-files/documentation/index.html` → documentación de la plantilla Roksyn, no es
>   parte del sistema de negocio.
>
> En adelante, todas las rutas de archivo se expresan **relativas a `main-files/roksyn/`**
> salvo que se indique lo contrario.

---

## 1. Resumen general

| Métrica | Valor |
|---|---:|
| Archivo raíz analizado | `index.html` (`main-files/roksyn/index.html`) |
| Archivos `.html` totales en `main-files/roksyn/` | 183 |
| Pantallas de negocio (excluyendo demos de plantilla) | 109 |
| Pantallas de demo de plantilla Roksyn (ruido) | 74 |
| Pantallas de negocio **alcanzables** desde `index.html` | **68** |
| Pantallas de negocio **huérfanas** (no alcanzables) | **41** |
| Demos de plantilla alcanzables (arrastradas por links basura) | ~74 |
| Total de links `href` revisados | 18,988 |
| Links a `.html` revisados | 6,148 |
| Links `href="#"` (placeholder/ancla) | 612 |
| Links `href="javascript:;"` (sin destino real) | 9,855 |
| Links rotos a `.html` (archivo destino inexistente, solo páginas de negocio) | **120** |
| Acciones sin destino (placeholders `#` / `javascript:;` en botones/anchors de negocio) | cientos (ver §6) |
| Disparadores de modal detectados (páginas de negocio) | 374 |
| Disparadores de tabs/pills (páginas de negocio) | 155 |
| Bloques de acordeón detectados (páginas de negocio) | 501 |

**Interpretación rápida:**

1. La maqueta es la plantilla **Roksyn / Bootstrap 5 Admin**, sobre la que se construyeron
   las pantallas de negocio (nombres en español). Las **74 páginas demo originales**
   (`app-*`, `auth-*`, `component-*`, `ecommerce-*`, `form-*`, `charts-*`, `icons-*`,
   `map-*`, `pages-*`, `table-*`, `widget-*`, `timeline`, `faq`, `pricing-table`,
   `user-profile`, `index2`) **siguen presentes** y se cuelan en la navegación a través de
   links "Submódulo" basura dentro de `SCarga.html` y `Modulos.html`. Son ruido y deben
   tratarse como tales.
2. El menú lateral es la columna vertebral de la navegación y es prácticamente idéntico en
   todas las páginas. Por eso casi todas las páginas "apuntan" entre sí (predecesores
   masivos); lo que aporta valor real son los **links del área de contenido** (tablas,
   botones de acción, tabs y modales), que es lo que este documento detalla.
3. Hay una gran cantidad de **versiones/duplicados abandonados** del módulo de Parámetros y
   de Forecast (`ParametrosViejos`, `ParametrosViejos20`, `Parametrosversion2`,
   `Parametrosactuales`, `SketchVerParametros`, `posibleParametrosViejos (1..5)`,
   `ForecastActivo`, `ForecastActivo22`, `ForecastPresupuestal`, `EditForecast`,
   `NuevoForecast`) y un set completo de **wireframes** `Sketch*` (≈21 archivos) que viven
   aislados del `index.html`.

---

## 2. Menú principal y árbol global de navegación

El menú lateral (`<ul id="menu">` en `index.html`) es el árbol de navegación global. Se
reproduce literalmente abajo (texto del menú → destino real en el HTML).

### Menú principal (sidebar)

- **Home** → `index.html`
- **Forecast** → `SIPRES.html`  *(ícono "redeem"; el menú dice "Forecast" pero el archivo
  se llama SIPRES)*
- *Etiqueta: Gestion de Presupuestos*
- **Planeacion Presupuestal** *(desplegable)*
  - Parametros → `Parametros.html`
  - **Base Presupuestal** *(sub-desplegable)*
    - Base del Ejercicio Activo → `BPresupuestal.html`
    - Registro de Bases Presupuestales → `javascript:;`  ⚠️ **sin destino** (existe
      `BPRegistros.html`, pero el menú no lo enlaza)
  - Carga Presupuestal → `SelGrupoEmpresarial.html`
  - Autorizaciones → `Autorizaciones.html`
  - Liberaciones → `Liberaciones.html`
- **Ejercicio Presupuestal** *(desplegable)*
  - Movimientos Presupuestales → `" SCarga.html"`  ⚠️ **href con espacio inicial** (resuelve
    a `SCarga.html` por tolerancia del navegador, pero está malformado)
- *Etiqueta: Configuracion General*
- **Sistema** *(desplegable)*
  - Usuarios/Perfiles → `PUsuarios.html`
  - Centros de Costos → `CeCos.html`
  - Grupo de Cuentas → `GCuentas.html`
  - Campañas Transversales → `CTransversal.html`
  - Proyectos → `PFondo.html`

### Selector de perfiles (botón "Perfiles" en el breadcrumb del Home)

Dropdown que simula el cambio de perfil de usuario; cada opción abre un "Home" distinto:

- Carga de presupuesto → `P2.html`
- Carga / autoriza Mkt → `P3.html`
- Carga/autoriza Marketing → `P4.html`
- Autorizador de Marketing → `P5.html`
- Gerencia Admon&Fin.Mkt → `HomeP1.html`
- Autorizador de Marca → `P6.html`
- Autorizador de Oferteo → `P7.html`
- Autorizador de Estrategia → `P8.html`
- Autorizador de Mkt → `P9.html`
- Administración presupuesto → `P10.html`
- Admon Sistema → `P11.html`

### Árbol de negocio alcanzable desde `index.html` (resumido)

```
index.html (Home / perfil HomeP1)
├─ [Perfiles] P2..P11, HomeP1            (homes de perfil; en su mayoría hojas sin flujo)
│
├─ Forecast → SIPRES.html
│   └─ ForecastDetalle.html
│       └─ (BPRegistros.html)
│
├─ Planeacion Presupuestal
│   ├─ Parametros.html
│   │   ├─ Parametrosactuales.html ("2027" / Ver Detalle / Aperturar Ejercicio)
│   │   ├─ ParametrosViejos.html ("Editar")
│   │   └─ Reportes.html
│   ├─ Base del Ejercicio Activo → BPresupuestal.html
│   │   ├─ BPRegistros.html → BPCerrada.html
│   │   └─ BPCalculada.html → BPV1.html
│   ├─ Carga Presupuestal → SelGrupoEmpresarial.html
│   │   ├─ AEjercicio_BackOffice.html
│   │   ├─ AEjercicio_GrupoElektra.html
│   │   └─ AEjercicio_Totalplay.html
│   │        ├─ (tabla solicitudes) → PMktBorradorNormal / PMktPendienteNormal /
│   │        │     PMktAjustesNormal / PMktRechazada / PMktAprobada
│   │        │     + 9 estados ROTOS (PMkt*Bloqueado/Permitido/Excedente, PInver*)
│   │        ├─ Crear Ordinario → NuevaSol_Ordinario.html
│   │        └─ Crear Inversión → NuevaSol_Inversion.html
│   ├─ Autorizaciones → Autorizaciones.html
│   │   ├─ AutorizacionN1/N2/N3.html
│   │   ├─ AutorizacionExcedente.html / AutorizacionExcedente2.html / AutorizacionRemanente.html
│   │   ├─ DetalleAprobada.html / DetalleRechazada.html
│   │   └─ SolAprob.html
│   └─ Liberaciones → Liberaciones.html  → (modal "Exponer a SIPRES")
│
├─ Ejercicio Presupuestal
│   └─ Movimientos Presupuestales → SCarga.html
│       ├─ Modulos.html
│       ├─ Forecast.html  ⚠️ ROTO
│       └─ Submódulos 4.x/5.x/6.x → demos de plantilla (icons-*, form-elements, table-*)  ⚠️ ruido
│
├─ (flujo de captura paralelo, alcanzable por contenido) ReportesPPTO.html
│   ├─ Nueva Solicitud → NuevaSol.html
│   ├─ F-26001 → NuevaCarga.html
│   ├─ F-20232 → SolCorrecta.html
│   ├─ F-26002 → VerSolicitud.html
│   ├─ F-26003 → AjusteSol.html
│   ├─ F-26004 → SolAprob.html
│   └─ F-26005 → RechazarSol.html
│
└─ Sistema
    ├─ Usuarios/Perfiles → PUsuarios.html
    │   ├─ Nueva Relacion → NewUser.html
    │   ├─ (fila) → DetalleUsuario.html → EditarUsuario.html / DuplicarUsuario.html
    │   └─ (fila) → DuplicarUsuario.html
    ├─ Centros de Costos → CeCos.html       (acordeones de jerarquía)
    ├─ Grupo de Cuentas → GCuentas.html
    │   ├─ Nueva Cuenta → NuevaCuenta.html
    │   └─ (fila) → DetalleCuenta.html → EditarCuenta.html
    ├─ Campañas Transversales → CTransversal.html  (modales Alta/Editar/Eliminar)
    └─ Proyectos → PFondo.html              (modales Proyecto/Detalle/Editar/Eliminar)
```

---

## 3. Árbol detallado por pantalla

> Se documentan en detalle los **hubs y pantallas clave de cada flujo**. Los clusters
> repetitivos (homes de perfil `P2..P11`, estados de detalle `PMkt*`, wireframes `Sketch*`,
> borradores `posibleParametrosViejos`) se documentan agrupados al final de esta sección y
> en §5 (huérfanos).
>
> En toda la maqueta el **menú lateral** y el **modal de búsqueda** (`#exampleModal`) son
> componentes compartidos; no se repiten en cada ficha salvo cuando hay desviaciones.

---

## index.html — Home / Perfil Gerencia Admon&Fin.Mkt

- Archivo: `index.html`
- Módulo: `Home`
- Épica relacionada: `Transversal (entrada / selección de perfil)`
- Acceso desde: nodo raíz (todas las páginas vuelven aquí vía logo/Home)
- Tipo de pantalla: `tablero / home`

### Elementos de navegación detectados
- Breadcrumb: Sí ("Home")
- Menú local (sidebar): Sí (menú maestro descrito en §2)
- Tabs: No
- Acordeones: No
- Modales: solo `#exampleModal` (búsqueda, boilerplate)

### Acciones de navegación
| Elemento | Texto / ícono | Tipo | Destino actual | Destino esperado | Observaciones |
|---|---|---:|---|---|---|
| Dropdown "Perfiles" | Carga de presupuesto | link | `P2.html` | `P2.html` | correcto |
| Dropdown "Perfiles" | Gerencia Admon&Fin.Mkt | link | `HomeP1.html` | `HomeP1.html` | correcto |
| Dropdown "Perfiles" | (P3..P11) | link | `P3..P11.html` | igual | correctos |
| Sidebar | (todo el menú) | link | ver §2 | ver §2 | 2 entradas rotas (ver §2/§6) |

### Flujo representado
Punto de entrada y selección de perfil. La card central describe las capacidades del perfil
"Gerencia Administración y Finanzas Mkt". No hay tablas ni acciones de negocio aquí.

### Problemas detectados
- El menú lateral arrastra dos defectos globales (heredados a todas las páginas): "Registro
  de Bases Presupuestales" → `javascript:;` y "Movimientos Presupuestales" → `" SCarga.html"`
  con espacio inicial.
- `index.html` (título `Home P1`) es casi idéntico a `HomeP1.html`: posible duplicación de
  home.

---

## SIPRES.html — Forecast

- Archivo: `SIPRES.html`
- Módulo: `Planeación Presupuestal / Forecast`
- Épica relacionada: `E7 (Forecast / base presupuestal)`
- Acceso desde: `index.html` (menú "Forecast")
- Tipo de pantalla: `listado / tablero de forecast`

### Elementos de navegación detectados
- Breadcrumb: Sí ("Planeación Presupuestal" → `Inicio.html` ⚠️ roto)
- Tabs: No · Acordeones: No
- Modales disparados: Sí (`#modalCargarForecast`, `#modalEliminarForecast`)

### Acciones de navegación
| Elemento | Texto / ícono | Tipo | Destino actual | Destino esperado | Observaciones |
|---|---|---:|---|---|---|
| Link tabla | (fila forecast) | link | `ForecastDetalle.html` | `ForecastDetalle.html` | correcto |
| Botón | Cargar Forecast | modal | `#modalCargarForecast` | modal de carga | OK (sin backend) |
| Botón ícono | (eliminar) | modal | `#modalEliminarForecast` | modal confirmación | OK |
| Breadcrumb | Planeación Presupuestal | link | `Inicio.html` | `index.html` / `HomeP1.html` | **roto** |

### Flujo representado
Bandeja de forecast cargados; permite ver el detalle de un forecast y simular carga/eliminación.

### Problemas detectados
- Breadcrumb a `Inicio.html` (no existe).

---

## Parametros.html — Parámetros de Carga

- Archivo: `Parametros.html`
- Módulo: `Planeación Presupuestal / Parámetros`
- Épica relacionada: `E1 (Parámetros / Ejercicio presupuestal)`
- Acceso desde: `index.html` (menú "Parametros")
- Tipo de pantalla: `listado / catálogo de ejercicios`

### Elementos de navegación detectados
- Breadcrumb: No visible · Tabs: No · Acordeones: No
- Modales: `#modalNuevoEjercicio`

### Acciones de navegación
| Elemento | Texto | Tipo | Destino actual | Destino esperado | Observaciones |
|---|---|---:|---|---|---|
| Link | 2027 | link | `ParametrosActuales.html` | `Parametrosactuales.html` | **roto por mayúsculas** (el archivo es minúscula) |
| Botón | Ver Detalle | link | `Parametrosactuales.html` | `Parametrosactuales.html` | correcto |
| Botón | Aperturar Ejercicio | link | `Parametrosactuales.html` | (¿vista de apertura?) | reutiliza la misma pantalla |
| Botón | Editar | link | `ParametrosViejos.html` | (¿editor de parámetros?) | nombre ambiguo "Viejos" |
| Botón | Nuevo Ejercicio | modal | `#modalNuevoEjercicio` | modal alta | OK |
| Sidebar local | Reportes | link | `Reportes.html` | `Reportes.html` | correcto |

### Flujo representado
Catálogo de ejercicios presupuestales; alta/edición/apertura de ejercicio y acceso a su detalle.

### Problemas detectados
- `ParametrosActuales.html` vs `Parametrosactuales.html`: inconsistencia de mayúsculas → link
  roto en servidores sensibles a mayúsculas.
- "Editar" lleva a `ParametrosViejos.html`, nombre confuso (ver duplicados de Parámetros en §5).

---

## BPresupuestal.html — Base Presupuestal (Ejercicio Activo)

- Archivo: `BPresupuestal.html`
- Módulo: `Planeación Presupuestal / Base Presupuestal`
- Épica relacionada: `E7 (Carga de forecast y cálculo de base presupuestal)`
- Acceso desde: `index.html` (menú "Base del Ejercicio Activo")
- Tipo de pantalla: `tablero / estado de base (vacía)`

### Elementos de navegación detectados
- Breadcrumb: Sí ("Gestión de Base Presupuestal")
- Tabs: No · Acordeones: No
- Modales: `#modalGenerarBase`

### Acciones de navegación
| Elemento | Texto | Tipo | Destino actual | Destino esperado | Observaciones |
|---|---|---:|---|---|---|
| Link | Registro de Bases Presupuestales | link | `BPRegistros.html` | `BPRegistros.html` | correcto (aquí sí enlaza, a diferencia del menú global) |
| Botón | Calcular Base | link | `BPCalculada.html` | `BPCalculada.html` | correcto |
| Botón | Generar Base Presupuestal | modal | `#modalGenerarBase` | modal generación | OK |

### Flujo representado
Estado inicial (base vacía) → genera/calcula la base presupuestal del ejercicio activo.
Encadena con `BPCalculada.html` (base calculada) → `BPV1.html` (versión 1).

### Problemas detectados
- Ninguno crítico; el flujo de base está bien encadenado (`BPresupuestal → BPCalculada →
  BPV1`; `BPRegistros → BPCerrada`).

---

## BPRegistros.html / BPCalculada.html / BPV1.html / BPCerrada.html — Cadena de Base Presupuestal

- Módulo: `Planeación Presupuestal / Base Presupuestal` · Épica: `E7`
- Acceso desde: `BPresupuestal.html` (y links de contenido)
- Tipo: `listado` (BPRegistros, BPCerrada) / `detalle de versión` (BPCalculada, BPV1)

| Archivo | Acción clave | Destino | Observaciones |
|---|---|---|---|
| `BPRegistros.html` | (fila) Ver base cerrada | `BPCerrada.html` | correcto |
| `BPCalculada.html` | (fila) Ver versión | `BPV1.html` | correcto |
| `BPCalculada.html` | Generar Nueva Base | `#modalGenerarBase` | modal |
| `BPCalculada.html` | Restaurar versión | `#modalRestaurarVersion` | modal |
| `BPV1.html` | — | — | hoja de detalle |
| `BPCerrada.html` | — | — | hoja de detalle (Base Histórica 2025) |

### Problemas detectados
- `BPRegistros.html` **no está enlazado desde el menú** (la entrada "Registro de Bases
  Presupuestales" del sidebar es `javascript:;`). Solo se llega por links de contenido.

---

## SelGrupoEmpresarial.html — Carga Presupuestal: Selección de Grupo

- Archivo: `SelGrupoEmpresarial.html`
- Módulo: `Planeación Presupuestal / Carga Presupuestal`
- Épica relacionada: `E8 (Carga presupuestal)`
- Acceso desde: `index.html` (menú "Carga Presupuestal")
- Tipo de pantalla: `selector / hub de cards`

### Elementos de navegación detectados
- Breadcrumb: No · Tabs: No · Acordeones: No · Modales: solo búsqueda

### Acciones de navegación
| Elemento | Texto | Tipo | Destino actual | Destino esperado | Observaciones |
|---|---|---:|---|---|---|
| Card | Back Office | link | `AEjercicio_BackOffice.html` | igual | correcto |
| Card | Grupo Elektra | link | `AEjercicio_GrupoElektra.html` | igual | correcto |
| Card | Totalplay | link | `AEjercicio_Totalplay.html` | igual | correcto |

### Flujo representado
Primer paso de la **Carga Presupuestal (E8)**: el usuario elige el grupo empresarial y entra
al ejercicio de carga correspondiente.

### Problemas detectados
- No existe una card/variante "AEjercicio.html" genérica desde aquí, aunque ese archivo
  existe y es prácticamente el mismo que las tres variantes (posible duplicado base).

---

## AEjercicio_*.html (BackOffice / GrupoElektra / Totalplay) y AEjercicio.html — Ejercicio de Carga

- Archivos: `AEjercicio_BackOffice.html`, `AEjercicio_GrupoElektra.html`,
  `AEjercicio_Totalplay.html`, `AEjercicio.html`
- Módulo: `Carga Presupuestal` · Épica: `E8 (Carga presupuestal)`
- Acceso desde: `SelGrupoEmpresarial.html` (las 3 variantes con sufijo). `AEjercicio.html`
  (sin sufijo) se alcanza solo de vuelta desde las pantallas de detalle `PMkt*`.
- Tipo de pantalla: `listado de solicitudes + tablero`

### Elementos de navegación detectados
- Breadcrumb: No · Tabs: Sí (3) · Acordeones: No
- Modales: `#modalTipoSolicitud`, `#modalReporteCarga`, `#modalConfirmarEliminacion`,
  `#filtrosAvanzados`, `#filtrosAvanzadosResumen` (18 bloques `modal` en total)

### Tabla de la pantalla — Solicitudes de carga (folios F-260xx)
- Columnas relevantes: Folio, estado, importes, acciones.
- Acciones por fila (link en folio):

| Folio (texto) | Destino actual | ¿Existe? | Observaciones |
|---|---|:--:|---|
| F-26001 | `PMktBorradorNormal.html` | ✅ | correcto |
| F-26002 | `PMktBorradorBloqueado.html` | ❌ | **roto** |
| F-26003 | `PMktBorradorPermitido.html` | ❌ | **roto** |
| F-26004 | `PMktPendienteNormal.html` | ✅ | correcto |
| F-26005 | `PMktPendienteExcedente.html` | ❌ | **roto** |
| F-26006 | `PMktAjustesNormal.html` | ✅ | correcto |
| F-26007 | `PMktAjustesExcedente.html` | ❌ | **roto** |
| F-26008 | `PMktRechazada.html` | ✅ | correcto |
| F-26009 | `PMktAprobada.html` | ✅ | correcto |
| F-26010 | `PInverBorrador.html` | ❌ | **roto** |
| F-26011 | `PInverPendiente.html` | ❌ | **roto** |
| F-26012 | `PInverAjustes.html` | ❌ | **roto** |
| F-26013 | `PInverRechazada.html` | ❌ | **roto** |
| F-26014 | `PInverAprobada.html` | ❌ | **roto** |

### Acciones de navegación (CTA)
| Elemento | Texto | Tipo | Destino actual | Observaciones |
|---|---|---:|---|---|
| Botón | Nueva Solicitud | modal | `#modalTipoSolicitud` | abre selector de tipo |
| (en modal) | Crear (Ordinario) | link | `NuevaSol_Ordinario.html` | correcto |
| (en modal) | Crear (Inversión) | link | `NuevaSol_Inversion.html` | correcto |
| Botón | Descargar Reporte | modal | `#modalReporteCarga` | OK |
| Ícono fila | (eliminar) | modal | `#modalConfirmarEliminacion` | OK |

### Flujo representado
Núcleo de la **Carga Presupuestal (E8)**: bandeja de solicitudes por grupo, con estados
(Borrador / Pendiente / Ajustes / Rechazada / Aprobada) tanto para gasto **Mkt** como para
**Proyectos de Inversión (PInver)**. Da de alta solicitudes Ordinarias y de Inversión.

### Problemas detectados (alta prioridad)
- **9 de 14 estados de la tabla apuntan a archivos inexistentes** (`PMkt*Bloqueado`,
  `PMkt*Permitido`, `PMkt*Excedente`, y los 5 `PInver*`). Solo 5 detalles existen
  (`PMktBorradorNormal`, `PMktPendienteNormal`, `PMktAjustesNormal`, `PMktRechazada`,
  `PMktAprobada`). Esto multiplica los links rotos por las 4 variantes (≈73 instancias).
- `AEjercicio.html` (sin sufijo) parece ser la base de la que derivan las 3 variantes →
  posible duplicado; no cuelga del selector pero sí recibe regresos desde `PMkt*`.

---

## PMktBorradorNormal / PMktPendienteNormal / PMktAjustesNormal / PMktRechazada / PMktAprobada — Detalle de Solicitud

- Módulo: `Carga Presupuestal` · Épica: `E8` (y `E9` para Aprobada/Rechazada)
- Acceso desde: `AEjercicio*.html` (links de folio)
- Tipo de pantalla: `detalle de solicitud`
- Navegación: Tabs Sí (3) · Acordeones Sí (11) · Modales en estados editables
  (`PMktBorradorNormal`, `PMktAjustesNormal` tienen 7 bloques modal; los demás solo búsqueda)
- Regreso: vuelven a `AEjercicio.html` (no a la variante de origen) → ligera incoherencia.

### Flujo representado
Vista de detalle de una solicitud de carga según su estado. Representan los distintos
"momentos" del ciclo de vida de la solicitud (borrador, pendiente, en ajustes, rechazada,
aprobada).

### Problemas detectados
- Solo existen los 5 estados "Normal/Rechazada/Aprobada"; faltan los estados "Bloqueado",
  "Permitido", "Excedente" e **todos los de Inversión** (`PInver*`) que la tabla referencia.
- El botón de regreso no respeta el grupo de origen (siempre `AEjercicio.html`).

---

## NuevaSol_Ordinario.html y NuevaSol_Inversion.html — Alta de Solicitud

- Módulo: `Carga Presupuestal` · Épica: `E8`
- Acceso desde: `AEjercicio*.html` (modal "Nueva Solicitud" → "Crear")
- Tipo de pantalla: `formulario / wizard`
- Navegación: Acordeones Sí (5) · Modales numerosos (39 / 32 bloques) de validación y envío
  (`#modalValidacion`, `#modalQuitarCeco`, `#modalBorrador`, `#modalBorradorExito`,
  `#modalCancelar`, `#modalConfirmarEnvio`, `#modalEnvioBloqueado`, `#modalEnvio`,
  `#modalNuevoProyecto` en Inversión)

### Flujo representado
Captura de una nueva solicitud de carga, ordinaria o de proyecto de inversión, con
distribución por CeCo, guardado de borrador y envío a autorización (modales de confirmación).

### Problemas detectados
- Los modales de envío son terminales (no navegan a otra pantalla): el flujo de "envío
  exitoso → bandeja de autorizaciones" queda **truncado** (no hay link de salida real a
  `Autorizaciones.html`).
- Detalle técnico: hay marcadores de plantilla `${c.num}`/`${c.nombre}` en disparadores de
  modal (placeholders de un render JS que no corre); irrelevante para negocio pero conviene
  saberlo.

---

## Autorizaciones.html — Autorizaciones de Carga

- Archivo: `Autorizaciones.html`
- Módulo: `Planeación Presupuestal / Autorizaciones`
- Épica relacionada: `E9 (Autorizaciones)`
- Acceso desde: `index.html` (menú "Autorizaciones")
- Tipo de pantalla: `bandeja de autorización / tablero jerárquico`

### Elementos de navegación detectados
- Breadcrumb: No · Tabs: Sí (3) · Acordeones: Sí (18)
- Modales: `#modalEstrategia`, `#modalDescargaResumen` (+ collapses de jerarquía por columna)

### Tabla / bandeja — Solicitudes a autorizar (folios NMX y GP/CP/EXC)
| Folio (texto) | Destino actual | ¿Existe? | Observaciones |
|---|---|:--:|---|
| F-26002NMX | `AutorizacionExcedente.html` | ✅ | correcto |
| F-26002NMX | `AutorizacionExcedente2.html` | ✅ | correcto |
| F-26002NMX | `AutorizacionRemanente.html` | ✅ | correcto |
| F-26003NMX | `AutorizacionN1.html` | ✅ | correcto |
| F-26001NMX | `AutorizacionN2.html` | ✅ | correcto |
| F-26004NMX | `AutorizacionN3.html` | ✅ | correcto |
| F-25088NMX | `DetalleAprobada.html` | ✅ | correcto |
| F-26005NMX | `DetalleRechazada.html` | ✅ | correcto |
| GP/CP-2026-… | `SolAprob.html` | ✅ | correcto |
| EXC-2026-015/018 | `AutorizacionExcedente.html` | ✅ | correcto |

### Acciones de navegación
| Elemento | Texto | Tipo | Destino | Observaciones |
|---|---|---:|---|---|
| Botón | Estrategia de Autorización | modal | `#modalEstrategia` | OK |
| Botón | Exportar Matriz Contable | modal | `#modalDescargaResumen` | OK |
| Acordeón | columnas país/división/CeCo | collapse | `#col-*` | jerarquía expandible |

### Flujo representado
Bandeja central de **Autorizaciones (E9)**: revisión por niveles (N1/N2/N3), manejo de
excedentes/remanentes (vínculo con **E12 ajustes especiales**) y consulta de detalle
aprobado/rechazado.

### Problemas detectados
- Las pantallas de detalle de autorización (`AutorizacionN1/N2/N3`, `DetalleAprobada`,
  `ForecastPresupuestal`) intentan **regresar a `BandejaAutorizaciones.html`, que no existe**
  → 19 instancias rotas. El destino correcto es `Autorizaciones.html`.

---

## AutorizacionN1/N2/N3, AutorizacionExcedente(2), AutorizacionRemanente, DetalleAprobada, DetalleRechazada

- Módulo: `Autorizaciones` · Épica: `E9` (+ `E12` para Excedente/Remanente)
- Acceso desde: `Autorizaciones.html` (y `Liberaciones.html`)
- Tipo: `detalle de autorización`
- Navegación: Tabs Sí (2) · Modales numerosos (21–29 bloques: aprobar/rechazar/observaciones)

### Problemas detectados
- `AutorizacionN1/N2/N3.html` y `DetalleAprobada.html` → `BandejaAutorizaciones.html`
  (**inexistente**, debe ser `Autorizaciones.html`).
- `AutorizacionExcedente.html` y `AutorizacionExcedente2.html` parecen el mismo paso
  duplicado (mismo título "Excedente"); `AutorizacionRemanente.html` también comparte
  título "Excedente" pese al nombre.

---

## Liberaciones.html — Liberación de Presupuesto a SIPRES

- Archivo: `Liberaciones.html`
- Módulo: `Planeación Presupuestal / Liberaciones`
- Épica relacionada: `E10 (Liberación de presupuesto a SIPRES)`
- Acceso desde: `index.html` (menú "Liberaciones")
- Tipo de pantalla: `tablero con tabs (aprobadas/pendientes/SIPRES/bitácora)`

### Elementos de navegación detectados
- Breadcrumb: Sí ("Liberación de Presupuesto" → `HomeP1.html`)
- Tabs: Sí (`#tab-aprobadas`, `#tab-pendientes`, `#tab-sipres`, `#tab-bitacora`)
- Acordeones: Sí (92 collapses de jerarquía país/sector/unidad)
- Modales: `#modalLiberar` ("Exponer a SIPRES")

### Acciones de navegación
| Elemento | Texto | Tipo | Destino actual | Observaciones |
|---|---|---:|---|---|
| Tab | Presupuesto Aprobado / Pendiente / Última Versión Sincronizada / Bitácora | tab | `#tab-*` | correcto |
| Botón | Exponer a SIPRES | modal | `#modalLiberar` | OK (simula sincronización) |
| Link folio | F-26005NMX | link | `AutorizacionExcedente.html` | correcto |
| Link folio | F-26008GTM | link | `AutorizacionN2.html` | correcto |
| Link folio | F-26015NMX | link | `AutorizacionN3.html` | correcto |
| Link folio | F-26012HND | link | `AutorizacionN1.html` | correcto |

### Flujo representado
Cierre del ciclo: **Liberación a SIPRES (E10)**. Muestra presupuesto aprobado vs. pendiente,
la última versión sincronizada con SIPRES y una pestaña de **bitácora** (la "Bitácora de
Liberación" es un tab interno, no una pantalla aparte).

### Problemas detectados
- La "Bitácora" existe solo como tab interno; no hay pantalla/archivo de bitácora dedicada.
- `modalLiberar` es terminal (no enlaza a `SIPRES.html`); el cierre "liberar → ver en SIPRES"
  queda como simulación dentro del modal.

---

## SCarga.html y Modulos.html — Ejercicio Presupuestal / Configuración de Módulos

- Archivos: `SCarga.html`, `Modulos.html`
- Módulo: `Ejercicio Presupuestal` · Épica: `E1 (Ejercicio presupuestal)` *(probable)*
- Acceso desde: `index.html` (menú "Movimientos Presupuestales" → `SCarga.html`); `Modulos`
  desde `SCarga`.
- Tipo de pantalla: `tablero de configuración`

### Acciones de navegación
| Elemento | Texto | Tipo | Destino actual | Observaciones |
|---|---|---:|---|---|
| Sidebar local | Forecast | link | `Forecast.html` | ❌ **roto** (no existe) |
| Sidebar local | Config. Módulos | link | `Modulos.html` | correcto |
| Sidebar local | Submódulo 4.1/4.2/4.3 | link | `icons-line-icons.html` / `icons-boxicons.html` / `icons-feather-icons.html` | ⚠️ **demos de plantilla** (ruido) |
| Sidebar local | Submódulo 5.1 | link | `form-elements.html` | ⚠️ demo de plantilla |
| Sidebar local | Submódulo 6.1/6.2 | link | `table-basic-table.html` / `table-datatable.html` | ⚠️ demo de plantilla |

### Flujo representado
Configuración de módulos del ejercicio. **Es el "puente" que contamina la navegación**: sus
"Submódulos" enlazan a las páginas demo originales de Roksyn, que a su vez (vía su propio
menú) hacen alcanzable todo el set de demos (`app-*`, `component-*`, `ecommerce-*`, etc.).

### Problemas detectados
- `Forecast.html` no existe (probable destino: `SIPRES.html` o `ForecastActivo.html`).
- 6 "Submódulos" apuntan a páginas demo de plantilla → ruido de navegación que debe
  desconectarse o reemplazarse por pantallas reales.

---

## ReportesPPTO.html — Carga de Presupuesto (bandeja de solicitudes, flujo alterno)

- Archivo: `ReportesPPTO.html`
- Módulo: `Carga Presupuestal / Reportes` · Épica: `E8` (captura) / reportes
- Acceso desde: links de contenido (`Liberaciones`, `AjusteSol`, `NuevaCarga`, etc.). **No
  cuelga directamente del menú lateral.**
- Tipo de pantalla: `listado de solicitudes con acciones`

### Tabla — Solicitudes (folios F-260xx)
| Folio | Destino | ¿Existe? | Observaciones |
|---|---|:--:|---|
| Nueva Solicitud (botón) | `NuevaSol.html` | ✅ | alta |
| F-26001 | `NuevaCarga.html` | ✅ | "tope excedido" |
| F-20232 | `SolCorrecta.html` | ✅ | solicitud OK |
| F-26002 | `VerSolicitud.html` | ✅ | ver |
| F-26003 | `AjusteSol.html` | ✅ | en ajustes |
| F-26004 | `SolAprob.html` | ✅ | aprobada |
| F-26005 | `RechazarSol.html` | ✅ | rechazo |
| Carga Masiva (botón) | `#modalCargaMasiva` | — | modal |

### Flujo representado
Bandeja **alternativa** de solicitudes (parece una versión paralela/anterior del flujo de
`AEjercicio*`). Encadena alta, ver, ajuste, aprobación y rechazo de solicitudes.

### Problemas detectados
- Coexiste con `AEjercicio*.html` representando **el mismo paso de negocio** (bandeja de
  solicitudes de carga) con distinto modelo de pantallas (`SolCorrecta/SolAprob/VerSolicitud/
  AjusteSol/RechazarSol/NuevaCarga/NuevaSol` vs `PMkt*`). Duplicidad de flujo a resolver con
  negocio.

---

## PUsuarios.html — Usuarios / Perfiles

- Archivo: `PUsuarios.html`
- Módulo: `Sistema / Usuarios` · Épica: `E6 (Usuarios y perfiles)`
- Acceso desde: `index.html` (menú "Usuarios/Perfiles")
- Tipo de pantalla: `listado / catálogo`

### Tabla — Relaciones Usuario/Perfil
- Acciones por fila:

| Acción | Destino actual | ¿Existe? | Observaciones |
|---|---|:--:|---|
| Nueva Relación Usuario/Perfil | `NewUser.html` | ✅ (vacío) | `NewUser.html` está **en blanco** (0 contenido) |
| (ver) | `DetalleUsuario.html` | ✅ | correcto |
| (duplicar) | `DuplicarUsuario.html` | ✅ | correcto |
| (eliminar) | `#modalConfirmarEliminar` | — | modal |

### Flujo representado
Catálogo de usuarios/perfiles (E6): alta, ver detalle, duplicar relación y eliminar.

### Problemas detectados
- `NewUser.html` está **vacío** (sin HTML útil): el alta de usuario queda truncada. Existen
  alternativas no enlazadas: `NuevaCuenta.html`/`EditarUsuario.html` (título "Nueva Relación
  de Usuario") podrían ser la pantalla real.
- `DetalleUsuario.html`, `EditarUsuario.html`, `DuplicarUsuario.html`, `EditarCuenta.html`
  tienen botón de regreso a `Inicio.html` (**inexistente** → debe ser `index.html`).
- Existe `PUsuarios-Detalle.html` **huérfano** (posible detalle alterno).

---

## DetalleUsuario / EditarUsuario / DuplicarUsuario — Subpantallas de Usuario (E6)

- Acceso desde: `PUsuarios.html` y entre ellas.
- Cadena: `PUsuarios → DetalleUsuario → EditarUsuario / DuplicarUsuario`.
- Problema común: regreso a `Inicio.html` (inexistente).

---

## CeCos.html — Centros de Costos

- Archivo: `CeCos.html`
- Módulo: `Sistema / Catálogos` · Épica: `E1` *(probable — configuración previa)*
- Acceso desde: `index.html` (menú "Centros de Costos")
- Tipo de pantalla: `catálogo jerárquico (acordeones)`

### Elementos de navegación detectados
- Breadcrumb: Sí ("Catálogos") · Tabs: Sí (4) · Acordeones: Sí (27)
- Modales: solo búsqueda

### Acciones
| Elemento | Texto | Tipo | Destino | Observaciones |
|---|---|---:|---|---|
| Acordeón | 6864 - TV AZTECA / 6863 - GRUPO ELEKTRA / MARKETING MASIVO / DIGITAL / EVENTOS Y BTL | collapse | `#collapse*` | jerarquía expandible |
| Sidebar local | Reportes | link | `Reportes.html` | correcto |

### Flujo representado
Catálogo de Centros de Costo con su jerarquía organizacional. Pantalla de consulta; sin alta
de CeCo navegable (todo vive en acordeones).

### Problemas detectados
- No hay pantalla/acción de alta o detalle de CeCo navegable (a diferencia de Cuentas o
  Proyectos). El detalle de CeCo en base presupuestal existe **huérfano**: `DetalleCecoBase.html`.

---

## GCuentas.html — Grupo de Cuentas

- Archivo: `GCuentas.html`
- Módulo: `Sistema / Catálogos` · Épica: `E1` *(probable)*
- Acceso desde: `index.html` (menú "Grupo de Cuentas")
- Tipo de pantalla: `listado / catálogo`

### Tabla — Cuentas presupuestales
| Acción | Destino actual | ¿Existe? | Observaciones |
|---|---|:--:|---|
| Nueva Cuenta Presupuestal | `NuevaCuenta.html` | ✅ | alta |
| (ver) | `DetalleCuenta.html` | ✅ | → `EditarCuenta.html` |
| (inactivar) | `#modalInactivarCuenta` | — | modal |
| (activar) | `#modalActivarCuenta` | — | modal |
| (eliminar) | `#modalConfirmarEliminar` | — | modal |

### Flujo representado
Catálogo de cuentas (E1): alta, ver/editar detalle, activar/inactivar/eliminar.

### Problemas detectados
- `EditarCuenta.html` y `DetalleCuenta.html` tienen el mismo título "Detalle del CeCo - Base
  Presupuestal" (copiado de otra pantalla) → título incorrecto.
- `EditarCuenta.html` → regreso `Inicio.html` (inexistente).
- `NGCuenta.html` (Nuevo Grupo de Cuenta) está **huérfano** y enlaza a `GruposCuentas.html`
  (inexistente).

---

## CTransversal.html — Campañas Transversales

- Archivo: `CTransversal.html`
- Módulo: `Sistema` · Épica: `E1` *(probable — configuración / catálogos)*
- Acceso desde: `index.html` (menú "Campañas Transversales")
- Tipo de pantalla: `catálogo con CRUD por modales`

### Acciones
| Elemento | Texto | Tipo | Destino | Observaciones |
|---|---|---:|---|---|
| Botón | Nueva Campaña | modal | `#modalAltaCampana` | OK |
| Ícono fila | (editar) | modal | `#modalEditarCampana` | OK |
| Ícono fila | (eliminar) | modal | `#modalEliminarCampana` | OK |

### Flujo representado
Catálogo de campañas transversales con alta/edición/eliminación íntegramente por modales.

### Problemas detectados
- Existen variantes **huérfanas** `CTransversalHU3.html` y `CTransversalHU4.html` (títulos
  "Campañas Transversales - IPSO", parecen iteraciones más nuevas no enlazadas).

---

## PFondo.html — Proyectos

- Archivo: `PFondo.html`
- Módulo: `Sistema / Proyectos` · Épica: `E1` *(probable)*
- Acceso desde: `index.html` (menú "Proyectos")
- Tipo de pantalla: `catálogo con CRUD por modales`

### Acciones
| Elemento | Texto | Tipo | Destino | Observaciones |
|---|---|---:|---|---|
| Botón | Nuevo Proyecto | modal | `#modalProyectoFondo` | OK |
| Ícono fila | (detalle) | modal | `#modalDetalleProyecto` | OK |
| Ícono fila | (editar) | modal | `#modalEditarProyecto` | OK |
| Ícono fila | (eliminar) | modal | `#modalEliminarProyecto` | OK |

### Flujo representado
Catálogo de proyectos/fondos, CRUD por modales.

### Problemas detectados
- Ninguno crítico de navegación (CRUD autocontenido por modales).

---

## Homes de perfil: HomeP1.html y P2.html … P11.html

- Módulo: `Home` · Épica: `E6` *(perfiles)*
- Acceso desde: dropdown "Perfiles" en el breadcrumb del Home / `index.html`.
- Tipo de pantalla: `home/tablero por perfil`
- Navegación: replican el dropdown "Perfiles" (cada uno enlaza a los demás `P*`/`HomeP1`).
  Casi todos son **hojas** (sin tabla ni flujo), salvo:
  - `HomeP1.html`: home "Gerencia Admon&Fin.Mkt" (equivalente a `index.html`).
  - `P3.html`: tiene tablas, tabs y acordeones (6) y un link a `NuevaSol.html`; es el único
    `P*` con flujo de captura embebido.

### Problemas detectados
- `index.html` y `HomeP1.html` son redundantes (mismo título "Home P1").
- `P2,P4..P11` son prácticamente idénticos entre sí (homes vacíos); duplicación.

---

## Cluster de wireframes `Sketch*` (≈21 archivos)

- Módulo: `Prototipos / wireframes` · Épica: `Transversal (diseño)`
- Acceso desde: **ninguna ruta desde `index.html`** → todo el cluster es **huérfano**
  (ver §5). Se enlazan entre sí formando una maqueta paralela de baja fidelidad.
- Punto de entrada interno aparente: `SketchHome.html`.
- Pantallas: `SketchHome, SketchCarga, SketchAutor, SketchBase, SketchCampanas, SketchCeCo,
  SketchCuentas, SketchUsuario, SketchEditUsuario, SketchDupUsuario, SketchNuevoUsuario,
  SketchParametros, SketchEditarParametro, SketchVerParametros, SketchVerDetalleParametro,
  SketchProyecto, SketchProyectos, SketchForecast, SketchForecastDetalle, SketchLibera,
  SketchEjercicio`.
- Problema: cluster aislado del sistema "real". `SketchCuentas.html` enlaza 13× a
  `SketchEditCuenta.html` (**inexistente**). `SketchForecast.html` → `Inicio.html`.

---

## 4. Árbol por épica

> Clasificación basada en evidencia de la maqueta (nombres, títulos, menú y encadenamiento).
> Donde no hay certeza se marca **Épica probable / Pendiente de validación funcional**.

### Épica E1 — Parámetros / Ejercicio presupuestal
- Pantallas relacionadas (parámetros):
  - `Parametros.html`, `Parametrosactuales.html`, `ParametrosViejos.html`
  - Variantes huérfanas/duplicadas: `ParametrosViejos20.html`, `Parametrosversion2.html`,
    `SketchVerParametros.html`, `posibleParametrosViejos (1..5).html`
- Pantallas relacionadas (ejercicio / catálogos de configuración):
  - `SCarga.html`, `Modulos.html`, `CeCos.html`, `GCuentas.html` (+`NuevaCuenta`,
    `DetalleCuenta`, `EditarCuenta`, `NGCuenta`), `CTransversal.html`
    (+`CTransversalHU3/HU4`), `PFondo.html`
- Punto de entrada: `index.html` → menú "Parametros", "Movimientos Presupuestales" y "Sistema".
- Flujo visible: `Parametros → Parametrosactuales (Ver Detalle / Aperturar) ` ; catálogos
  `CeCos / GCuentas / CTransversal / PFondo` como configuración previa.
- Acciones principales: alta/edición/apertura de ejercicio; CRUD de catálogos.
- Vacíos detectados: enorme duplicación de "Parámetros"; `Forecast.html` roto en `SCarga`;
  "Submódulos" de `SCarga/Modulos` apuntan a demos de plantilla; sin alta de CeCo navegable.

### Épica E6 — Usuarios / Perfiles
- Pantallas: `PUsuarios.html`, `NewUser.html` (vacío), `DetalleUsuario.html`,
  `EditarUsuario.html`, `DuplicarUsuario.html`, `PUsuarios-Detalle.html` (huérfano);
  homes de perfil `HomeP1`, `P2..P11`.
- Punto de entrada: `index.html` → menú "Usuarios/Perfiles" + dropdown "Perfiles".
- Flujo visible: `PUsuarios → DetalleUsuario → EditarUsuario / DuplicarUsuario`.
- Acciones principales: alta (rota: `NewUser` vacío), ver, editar, duplicar, eliminar (modal).
- Vacíos detectados: alta vacía; regresos a `Inicio.html`; `PUsuarios-Detalle.html` huérfano.

### Épica E7 — Forecast y base presupuestal
- Pantallas: `SIPRES.html` (Forecast), `ForecastDetalle.html`, `BPresupuestal.html`,
  `BPRegistros.html`, `BPCalculada.html`, `BPV1.html`, `BPCerrada.html`.
- Huérfanas relacionadas: `ForecastActivo.html`, `ForecastActivo22.html`,
  `ForecastPresupuestal.html`, `EditForecast.html`, `NuevoForecast.html`,
  `BPresupuestal.html.html`, `SIPRES2.html`, `DetalleCecoBase.html`.
- Punto de entrada: `index.html` → menú "Forecast" y "Base del Ejercicio Activo".
- Flujo visible: `SIPRES → ForecastDetalle` ; `BPresupuestal → BPCalculada → BPV1` ;
  `BPRegistros → BPCerrada`.
- Acciones principales: cargar/eliminar forecast; generar/calcular/restaurar base.
- Vacíos detectados: `BPRegistros` no se enlaza desde el menú (entrada `javascript:;`);
  muchas pantallas de Forecast huérfanas y duplicadas; `SIPRES` breadcrumb roto a `Inicio.html`.

### Épica E8 — Carga Presupuestal
- Pantallas (flujo principal): `SelGrupoEmpresarial.html` → `AEjercicio_BackOffice/
  GrupoElektra/Totalplay.html` (+ `AEjercicio.html`) → detalles `PMkt*` →
  `NuevaSol_Ordinario.html` / `NuevaSol_Inversion.html`.
- Pantallas (flujo alterno/duplicado): `ReportesPPTO.html` → `NuevaSol.html`, `NuevaCarga.html`,
  `VerSolicitud.html`, `AjusteSol.html`, `SolCorrecta.html`, `SolAprob.html`,
  `RechazarSol.html`, `EditarCarga.html`.
- Punto de entrada: `index.html` → menú "Carga Presupuestal".
- Flujo visible: `SelGrupoEmpresarial → AEjercicio_* → (folio) PMkt* / Nueva Solicitud`.
- Acciones principales: alta ordinaria/inversión, ver detalle por estado, ajustar, enviar.
- Vacíos detectados: 9/14 estados rotos en `AEjercicio*`; envío de `NuevaSol_*` no enlaza a
  Autorizaciones (flujo truncado); duplicidad `AEjercicio*` ⟷ `ReportesPPTO`.

### Épica E9 — Autorizaciones
- Pantallas: `Autorizaciones.html` → `AutorizacionN1/N2/N3.html`, `DetalleAprobada.html`,
  `DetalleRechazada.html`, `SolAprob.html`; `RevisarAu.html` (huérfano).
- Punto de entrada: `index.html` → menú "Autorizaciones".
- Flujo visible: `Autorizaciones → (folio) AutorizacionNx / DetalleAprobada / DetalleRechazada`.
- Acciones principales: autorizar por nivel, aprobar/rechazar (modales), exportar matriz.
- Vacíos detectados: regreso a `BandejaAutorizaciones.html` (inexistente) en N1/N2/N3 y
  DetalleAprobada; `RevisarAu.html` huérfano (su pantalla de "Autorizar solicitud" no se enlaza).

### Épica E10 — Liberación de presupuesto a SIPRES
- Pantallas: `Liberaciones.html` (tabs aprobadas/pendientes/SIPRES/bitácora), `SIPRES.html`
  (versión sincronizada).
- Punto de entrada: `index.html` → menú "Liberaciones".
- Flujo visible: `Liberaciones → (folio) AutorizacionNx` ; `modalLiberar` ("Exponer a SIPRES").
- Acciones principales: liberar/exponer a SIPRES, ver versión sincronizada, bitácora (tab).
- Vacíos detectados: la liberación termina en modal (no navega a `SIPRES.html`); bitácora solo
  como tab interno, sin pantalla dedicada.

### Épica E12 — Ajustes especiales (excedentes / remanentes)
- Pantallas: `AutorizacionExcedente.html`, `AutorizacionExcedente2.html`,
  `AutorizacionRemanente.html`, `AjusteSol.html`.
- Punto de entrada: desde `Autorizaciones.html` y `Liberaciones.html` (folios EXC-*).
- Flujo visible: `Autorizaciones/Liberaciones → AutorizacionExcedente / Remanente`.
- Acciones principales: autorizar excedente/remanente como vía de excepción.
- Vacíos detectados: `Excedente` y `Excedente2` parecen el mismo paso duplicado;
  `AutorizacionRemanente` reusa el título "Excedente"; **Épica probable / Pendiente de
  validación funcional** respecto al alcance exacto de E12.

---

## 5. Archivos huérfanos

> Archivos `.html` de negocio **no alcanzables** desde `index.html` (41). Se excluyen las
> páginas demo de plantilla. Fuera de `main-files/roksyn/` también hay HTML sueltos
> (ver nota al final de esta sección).

| Archivo | Posible módulo/épica | Motivo por el que parece existir | Link sugerido desde dónde |
|---|---|---|---|
| `BPresupuestal.html.html` | E7 | doble extensión accidental; copia de Home P1 | (eliminar / no enlazar) |
| `CTransversalHU3.html` | E1 (Campañas) | iteración "IPSO" de Campañas Transversales | reemplazar/enlazar desde `CTransversal.html` |
| `CTransversalHU4.html` | E1 (Campañas) | iteración "IPSO" de Campañas Transversales | reemplazar/enlazar desde `CTransversal.html` |
| `DetalleCecoBase.html` | E7 | detalle de CeCo en base presupuestal | desde `BPCalculada.html` / `CeCos.html` |
| `EditForecast.html` | E7 | edición/previsualización de forecast | desde `SIPRES.html` / `ForecastDetalle.html` |
| `ForecastActivo.html` | E7 | tablero de forecast activo | desde `SIPRES.html` |
| `ForecastActivo22.html` | E7 | variante "Base Presupuestal Calculada - IPSO" | consolidar con `BPCalculada.html` |
| `ForecastPresupuestal.html` | E7/E9 | forecast → autorización | desde `SIPRES.html`; corregir `BandejaAutorizaciones` |
| `NuevoForecast.html` | E7 | alta de forecast | desde `SIPRES.html` (botón "Cargar Forecast") |
| `NGCuenta.html` | E1 (Cuentas) | alta de Grupo de Cuenta | desde `GCuentas.html`; corregir `GruposCuentas.html` |
| `PUsuarios-Detalle.html` | E6 | detalle alterno de usuario | consolidar con `DetalleUsuario.html` |
| `ParametrosViejos20.html` | E1 | versión vieja de parámetros | (consolidar / eliminar) |
| `Parametrosversion2.html` | E1 | versión 2 de parámetros | (consolidar / eliminar) |
| `SketchVerParametros.html` | E1 | wireframe de ver parámetros | (cluster Sketch) |
| `RevisarAu.html` | E9 | pantalla "Autorizar solicitud" | desde `Autorizaciones.html` |
| `SIPRES2.html` | E10 | variante de SIPRES / Home P1 | consolidar con `SIPRES.html` |
| `posibleParametrosViejos (1).html` | E1 | borrador "Parametros de Presupuesto" | (eliminar / consolidar) |
| `posibleParametrosViejos (2).html` | E7 | borrador "Previsualizar Forecast" | (eliminar / consolidar) |
| `posibleParametrosViejos (3).html` | E7 | borrador "Forecast activo" | (eliminar / consolidar) |
| `posibleParametrosViejos (4).html` | E7 | borrador "Forecast activo" (link `BandejaAutorizaciones` roto) | (eliminar / consolidar) |
| `posibleParametrosViejos (5).html` | E1 | borrador "Parametros de Presupuesto" | (eliminar / consolidar) |
| `SketchHome.html` | Prototipo | entrada del set de wireframes | (cluster Sketch aislado) |
| `SketchCarga.html` | Prototipo E8 | wireframe carga presupuestal | (cluster Sketch) |
| `SketchAutor.html` | Prototipo E9 | wireframe autorización | (cluster Sketch) |
| `SketchBase.html` | Prototipo E7 | wireframe base | (cluster Sketch) |
| `SketchCampanas.html` | Prototipo E1 | wireframe campañas | (cluster Sketch) |
| `SketchCeCo.html` | Prototipo E1 | wireframe CeCos | (cluster Sketch) |
| `SketchCuentas.html` | Prototipo E1 | wireframe cuentas (link `SketchEditCuenta` roto ×13) | (cluster Sketch) |
| `SketchUsuario.html` | Prototipo E6 | wireframe usuarios | (cluster Sketch) |
| `SketchEditUsuario.html` | Prototipo E6 | wireframe editar usuario | (cluster Sketch) |
| `SketchDupUsuario.html` | Prototipo E6 | wireframe duplicar usuario | (cluster Sketch) |
| `SketchNuevoUsuario.html` | Prototipo E6 | wireframe nuevo usuario | (cluster Sketch) |
| `SketchParametros.html` | Prototipo E1 | wireframe parámetros | (cluster Sketch) |
| `SketchEditarParametro.html` | Prototipo E1 | wireframe editar parámetro | (cluster Sketch) |
| `SketchVerDetalleParametro.html` | Prototipo E1 | wireframe ver detalle parámetro | (cluster Sketch) |
| `SketchProyecto.html` | Prototipo E1 | wireframe proyecto | (cluster Sketch) |
| `SketchProyectos.html` | Prototipo E1 | wireframe proyectos | (cluster Sketch) |
| `SketchForecast.html` | Prototipo E7 | wireframe forecast (link `Inicio` roto) | (cluster Sketch) |
| `SketchForecastDetalle.html` | Prototipo E7 | wireframe detalle forecast | (cluster Sketch) |
| `SketchLibera.html` | Prototipo E10 | wireframe liberación | (cluster Sketch) |
| `SketchEjercicio.html` | Prototipo E1 | wireframe ejercicio | (cluster Sketch) |

**Notas adicionales sobre huérfanos:**
- `NewUser.html` **sí está enlazado** (desde `PUsuarios.html`) pero está **vacío**: no es
  huérfano, es una pantalla "muerta".
- Páginas demo de plantilla huérfanas: `index2.html`, `pages-edit-profile.html`,
  `pages-starter-page.html` (ruido de plantilla; el resto de demos son alcanzables por el
  puente de `SCarga/Modulos`).
- **Fuera de `main-files/roksyn/`** existen además: `/NuevaSol_Inversion.html`,
  `/NuevaSolicitud.html` (raíz del repo) y `/main-files/documentation/index.html`. No forman
  parte del árbol navegable de la maqueta y parecen copias/borradores externos.

---

## 6. Links rotos o inconsistentes

> 120 instancias de links a `.html` cuyo archivo destino **no existe** (solo páginas de
> negocio como origen). Tabla consolidada por tipo de problema. Además, 612 `href="#"` y
> 9,855 `href="javascript:;"` actúan como placeholders/acciones sin destino real
> (comportamiento esperado en una maqueta, pero relevante donde deberían navegar).

| Archivo origen | Elemento | Texto visible / id | Link actual | Link sugerido | Tipo de problema | Comentario |
|---|---|---|---|---|---|---|
| `index.html` (y todo el menú) | sidebar | Registro de Bases Presupuestales | `javascript:;` | `BPRegistros.html` | acción sin destino | la pantalla existe pero el menú no la enlaza |
| `index.html` (y todo el menú) | sidebar | Movimientos Presupuestales | `" SCarga.html"` | `SCarga.html` | naming inconsistente | href con espacio inicial |
| `AEjercicio*.html` | link tabla | F-26002 | `PMktBorradorBloqueado.html` | crear o reasignar a estado existente | archivo inexistente | 8 instancias |
| `AEjercicio*.html` | link tabla | F-26003 | `PMktBorradorPermitido.html` | crear o reasignar | archivo inexistente | 8 instancias |
| `AEjercicio*.html` | link tabla | F-26005 | `PMktPendienteExcedente.html` | crear o reasignar | archivo inexistente | 8 instancias |
| `AEjercicio*.html` | link tabla | F-26007 | `PMktAjustesExcedente.html` | crear o reasignar | archivo inexistente | 8 instancias |
| `AEjercicio*.html` | link tabla | F-26010 | `PInverBorrador.html` | crear pantalla de inversión | archivo inexistente | 8 instancias |
| `AEjercicio*.html` | link tabla | F-26011 | `PInverPendiente.html` | crear | archivo inexistente | 8 instancias |
| `AEjercicio*.html` | link tabla | F-26012 | `PInverAjustes.html` | crear | archivo inexistente | 8 instancias |
| `AEjercicio*.html` | link tabla | F-26013 | `PInverRechazada.html` | crear | archivo inexistente | 8 instancias |
| `AEjercicio*.html` | link tabla | F-26014 | `PInverAprobada.html` | crear | archivo inexistente | 8 instancias |
| `AEjercicio_GrupoElektra.html` | link | (reporte) | `ReportesCarga.html` | `Reportes.html` / `ReportesPPTO.html` | archivo inexistente | 1 instancia |
| `AutorizacionN1/N2/N3.html` | botón regreso | Volver | `BandejaAutorizaciones.html` | `Autorizaciones.html` | archivo inexistente | 12 instancias |
| `DetalleAprobada.html` | botón regreso | Volver | `BandejaAutorizaciones.html` | `Autorizaciones.html` | archivo inexistente | 3 instancias |
| `ForecastPresupuestal.html` | botón | (autorizar) | `BandejaAutorizaciones.html` | `Autorizaciones.html` | archivo inexistente | 2 instancias (huérfano) |
| `posibleParametrosViejos (4).html` | botón | (autorizar) | `BandejaAutorizaciones.html` | `Autorizaciones.html` | archivo inexistente | 2 instancias (huérfano) |
| `SketchCuentas.html` | acción tabla | (editar cuenta) | `SketchEditCuenta.html` | crear wireframe | archivo inexistente | 13 instancias (cluster Sketch) |
| `SIPRES.html` | breadcrumb | Planeación Presupuestal | `Inicio.html` | `index.html` / `HomeP1.html` | archivo inexistente | 1 instancia |
| `SIPRES2.html` | breadcrumb | Planeación Presupuestal | `Inicio.html` | `index.html` | archivo inexistente | huérfano |
| `DetalleUsuario.html` | botón regreso | Inicio | `Inicio.html` | `index.html` | archivo inexistente | 1 instancia |
| `DuplicarUsuario.html` | botón regreso | Inicio | `Inicio.html` | `index.html` | archivo inexistente | 1 instancia |
| `EditarUsuario.html` | botón regreso | Inicio | `Inicio.html` | `index.html` | archivo inexistente | 1 instancia |
| `EditarCuenta.html` | botón regreso | Inicio | `Inicio.html` | `index.html` | archivo inexistente | 1 instancia |
| `SketchForecast.html` | botón regreso | Inicio | `Inicio.html` | `SketchHome.html` | archivo inexistente | 1 instancia |
| `SCarga.html` | sidebar local | Forecast | `Forecast.html` | `SIPRES.html` / `ForecastActivo.html` | archivo inexistente | 1 instancia |
| `Modulos.html` | sidebar local | Forecast | `Forecast.html` | `SIPRES.html` | archivo inexistente | 1 instancia |
| `SCarga.html` / `Modulos.html` | sidebar local | Submódulo 4.x/5.x/6.x | `icons-*` / `form-elements` / `table-*` | pantallas reales o quitar | navegación circular/ruido | demos de plantilla |
| `Parametros.html` | link | 2027 | `ParametrosActuales.html` | `Parametrosactuales.html` | naming inconsistente | mayúsculas (case-sensitive) |
| `EditarCarga.html` | link | (grupo cuentas) | `GCunetas.html` | `GCuentas.html` | naming inconsistente | typo "GCunetas" |
| `EditarCarga.html` | link | (proyectos) | `PFondos.html` | `PFondo.html` | naming inconsistente | typo "PFondos" |
| `NGCuenta.html` | link | (grupos cuentas) | `GruposCuentas.html` | `GCuentas.html` | archivo inexistente | huérfano |
| `ParametrosViejos.html` | link | Detalle | `Detalle.html` | `Parametrosactuales.html` | archivo inexistente | 1 instancia |
| `DetalleCecoBase.html` | link | (base) | `BasePresupuestal.html` | `BPresupuestal.html` | naming inconsistente | huérfano |
| `PUsuarios.html` | botón | Nueva Relacion Usuario/Perfil | `NewUser.html` | pantalla de alta real | flujo incompleto | `NewUser.html` está vacío |

**Duplicidades de flujo (mismo paso de negocio en varias páginas):**

| Paso de negocio | Páginas que lo representan | Tipo |
|---|---|---|
| Home Gerencia Admon&Fin.Mkt | `index.html` ≈ `HomeP1.html` | duplicidad |
| Bandeja de solicitudes de carga (E8) | `AEjercicio*` (`PMkt*`) vs `ReportesPPTO` (`SolAprob/SolCorrecta/VerSolicitud/AjusteSol/RechazarSol/NuevaCarga/NuevaSol`) | duplicidad de flujo |
| Parámetros (E1) | `Parametros`, `Parametrosactuales`, `ParametrosViejos`, `ParametrosViejos20`, `Parametrosversion2`, `SketchVerParametros`, `posibleParametrosViejos (1..5)` | duplicidad masiva |
| Forecast / base calculada (E7) | `BPCalculada` vs `ForecastActivo22` ("Base Presupuestal Calculada - IPSO"); `ForecastActivo`/`ForecastPresupuestal`/`posibleParametrosViejos (3/4)` | duplicidad |
| Autorización Excedente (E12) | `AutorizacionExcedente` ≈ `AutorizacionExcedente2` ≈ `AutorizacionRemanente` (mismo título) | duplicidad |
| Detalle de usuario (E6) | `DetalleUsuario` vs `PUsuarios-Detalle` | duplicidad |
| Campañas (E1) | `CTransversal` vs `CTransversalHU3` vs `CTransversalHU4` | duplicidad/iteraciones |
| Maqueta completa en baja fidelidad | cluster `Sketch*` paralelo al sistema real | duplicidad estructural |

---

## 7. Recomendaciones de corrección

> Plan concreto archivo por archivo para la **segunda fase** (solo navegación; sin cambiar
> diseño ni agregar lógica). Pendiente de tu confirmación antes de ejecutar.

### Prioridad alta (rompen flujos núcleo E8/E9 y el menú maestro)

1. **Menú global (`index.html` y todas las páginas que lo replican):**
   - "Registro de Bases Presupuestales": cambiar `javascript:;` → `BPRegistros.html`.
   - "Movimientos Presupuestales": corregir `" SCarga.html"` → `SCarga.html` (quitar espacio).
2. **`AEjercicio.html`, `AEjercicio_BackOffice.html`, `AEjercicio_GrupoElektra.html`,
   `AEjercicio_Totalplay.html`** (tabla de folios): resolver los **9 estados rotos**. Decidir
   con negocio si se crean las pantallas faltantes (`PMkt*Bloqueado/Permitido/Excedente`,
   `PInver*`) o si los folios se reapuntan a los 5 detalles existentes
   (`PMktBorradorNormal`, `PMktPendienteNormal`, `PMktAjustesNormal`, `PMktRechazada`,
   `PMktAprobada`).
3. **Regreso de autorizaciones**: en `AutorizacionN1/N2/N3.html` y `DetalleAprobada.html`
   (y huérfanos `ForecastPresupuestal.html`, `posibleParametrosViejos (4).html`),
   cambiar `BandejaAutorizaciones.html` → `Autorizaciones.html` (19 instancias).
4. **`PUsuarios.html` → alta de usuario**: `NewUser.html` está vacío. Reapuntar "Nueva
   Relación" a la pantalla de alta real (candidata: `EditarUsuario.html`/`NuevaCuenta.html`)
   o poblar `NewUser.html`.
5. **`SCarga.html` y `Modulos.html`**: corregir "Forecast" (`Forecast.html` → `SIPRES.html`) y
   **desconectar los "Submódulos"** que apuntan a demos de plantilla (`icons-*`,
   `form-elements`, `table-*`) para que la navegación no se contamine con páginas demo.
6. **Cerrar el flujo E8 truncado**: en `NuevaSol_Ordinario.html`/`NuevaSol_Inversion.html`,
   que el modal de envío exitoso ofrezca un link a `Autorizaciones.html` (continuidad de flujo).

### Prioridad media (consistencia y huérfanos relevantes)

7. **Regresos a `Inicio.html`** (inexistente) → `index.html`: en `DetalleUsuario.html`,
   `DuplicarUsuario.html`, `EditarUsuario.html`, `EditarCuenta.html`, `SIPRES.html`,
   `SIPRES2.html`, `SketchForecast.html` (→ `SketchHome.html`).
8. **Mayúsculas/typos de archivo**:
   - `Parametros.html`: `ParametrosActuales.html` → `Parametrosactuales.html`.
   - `EditarCarga.html`: `GCunetas.html` → `GCuentas.html`; `PFondos.html` → `PFondo.html`.
   - `NGCuenta.html`: `GruposCuentas.html` → `GCuentas.html`.
   - `DetalleCecoBase.html`: `BasePresupuestal.html` → `BPresupuestal.html`.
   - `ParametrosViejos.html`: `Detalle.html` → `Parametrosactuales.html`.
9. **Conectar huérfanos con valor de negocio**:
   - `RevisarAu.html` ("Autorizar solicitud") ← desde `Autorizaciones.html`.
   - `NGCuenta.html` (alta de grupo de cuenta) ← desde `GCuentas.html`.
   - `DetalleCecoBase.html` ← desde `BPCalculada.html` / `CeCos.html`.
   - Forecast: enlazar/consolidar `ForecastActivo.html`, `NuevoForecast.html`,
     `EditForecast.html` desde `SIPRES.html`.
10. **Decisión sobre duplicados de flujo E8**: definir con negocio si la bandeja oficial es
    `AEjercicio*` o `ReportesPPTO`, y deprecar la otra.

### Prioridad baja (limpieza, homologación, deuda técnica)

11. **Depurar borradores/duplicados** (no enlazados): `posibleParametrosViejos (1..5).html`,
    `ParametrosViejos20.html`, `Parametrosversion2.html`, `BPresupuestal.html.html`,
    `SIPRES2.html`, `ForecastActivo22.html` → archivar o eliminar (documentando el borrado).
12. **Cluster `Sketch*`**: decidir si se conserva como anexo de diseño o se retira del repo de
    la maqueta navegable; hoy solo se enlaza internamente y tiene su propio link roto
    (`SketchEditCuenta.html`).
13. **Homologar breadcrumbs y botones "Volver/Regresar"** a un destino consistente
    (`index.html`/hub de cada módulo).
14. **Retirar/aislar las páginas demo de plantilla Roksyn** (`app-*`, `auth-*`, `component-*`,
    `ecommerce-*`, `form-*`, `charts-*`, `icons-*`, `map-*`, `pages-*`, `table-*`, `widget-*`,
    etc.) del árbol navegable de negocio.
15. **Corregir títulos copiados**: `DetalleCuenta.html` y `EditarCuenta.html` muestran
    "Detalle del CeCo - Base Presupuestal" en lugar de un título de cuenta.

---

### Anexo — Metodología

- Nodo raíz: `main-files/roksyn/index.html`.
- Se construyó el grafo de enlaces parseando los atributos `href` de los 183 `.html` de
  `main-files/roksyn/`, resolviendo a nombre de archivo (ignorando `#ancla` y `?query`).
- Reachability por BFS desde `index.html`. Para el conteo "de negocio" no se atravesaron las
  páginas demo de plantilla (se reportan aparte como ruido).
- Componentes (modales, tabs/pills, acordeones, tablas) detectados por patrones de clases y
  atributos Bootstrap (`data-bs-toggle`, `class="modal/accordion"`, `<table>`).
- "Links rotos" = `href` a un `.html` cuyo archivo no existe en `main-files/roksyn/`,
  contabilizando solo páginas de negocio como origen (se excluyó el ruido de
  `pages-edit-profile.html`, demo de plantilla con decenas de links a páginas inexistentes).
