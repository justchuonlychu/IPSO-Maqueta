# Mapa de navegación de la maqueta — raíz `AEjercicio.html`

> Variante de la auditoría de navegación tomando como **nodo raíz `AEjercicio.html`**
> (en vez de `index.html`). Mismo alcance metodológico; solo cambia el **punto de partida**.
>
> **Nodo raíz analizado:** `main-files/roksyn/AEjercicio.html`
>
> `AEjercicio.html` es la pantalla **"Ejercicio de Carga Presupuestal"** (bandeja de
> solicitudes de un grupo empresarial). Es el **hub de la Épica E8 (Carga Presupuestal)**.
>
> **Documento complementario:** el mapa rooteado en `index.html` está en
> [`mapa-navegacion-maqueta.md`](./mapa-navegacion-maqueta.md). Las secciones de **archivos
> huérfanos (§5)**, **links rotos (§6)** y **recomendaciones (§7)** son las mismas en ambos
> documentos porque describen **el mismo grafo de la maqueta**; aquí se reproducen enfocadas
> al flujo de Carga.
>
> Rutas relativas a `main-files/roksyn/` salvo indicación contraria.

---

## 1. Resumen general

| Métrica | Valor |
|---|---:|
| Archivo raíz analizado | `AEjercicio.html` |
| Pantallas de negocio **alcanzables** desde `AEjercicio.html` | **68** |
| ¿Coincide con el alcance desde `index.html`? | **Sí** (mismo componente conexo: `AEjercicio` carga el menú lateral completo y enlaza de vuelta a `index.html`) |
| Pantallas de negocio **huérfanas** (no alcanzables) | **41** (idénticas al mapa de `index.html`) |
| Hijos directos de `AEjercicio.html` (links internos) | 24 (11 del flujo de carga + 13 del menú/perfil compartido) |
| Estados de la tabla de solicitudes | 14 folios → **5 existen, 9 rotos** |
| Links a `.html` rotos originados **en `AEjercicio.html`** | **18** (×4 con las variantes = ~73 instancias) |
| Modales en `AEjercicio.html` (bloques `modal`) | 18 (incl. `#modalTipoSolicitud`, `#modalReporteCarga`, `#modalConfirmarEliminacion`, filtros) |
| Tabs en `AEjercicio.html` | 3 |
| Acordeones en `AEjercicio.html` | 0 |

**Interpretación:**

1. Partir de `AEjercicio.html` **no reduce el alcance**: como toda página de la maqueta replica
   el menú lateral maestro, desde aquí se llega a las mismas 68 pantallas de negocio y a las
   mismas 74 demos de plantilla (ruido). Lo que cambia es que el **flujo de Carga (E8) queda
   como espina dorsal** y el resto del sistema cuelga del menú.
2. El valor diferencial de esta vista es el **detalle del flujo de carga** que nace aquí:
   selección de estado de solicitud, alta ordinaria/inversión y continuidad hacia
   autorización y liberación.
3. Los problemas más graves de toda la maqueta **se concentran precisamente en este nodo**: la
   tabla de folios apunta a 9 pantallas de estado inexistentes.

---

## 2. Menú/árbol global de navegación desde `AEjercicio.html`

`AEjercicio.html` incluye el mismo **menú lateral maestro** documentado en el mapa de
`index.html` (Home, Forecast→`SIPRES.html`, Planeación Presupuestal, Ejercicio Presupuestal,
Sistema). No se repite aquí; ver §2 de [`mapa-navegacion-maqueta.md`](./mapa-navegacion-maqueta.md).

Además del menú, `AEjercicio.html` tiene navegación **propia del área de contenido**:

```
AEjercicio.html  (Ejercicio de Carga Presupuestal — bandeja de solicitudes)
│
├─ Sidebar local del módulo
│   ├─ Registro de Bases Presupuestales → BPRegistros.html
│   └─ Reportes → Reportes.html
│
├─ Selector de perfil (cards)
│   ├─ Carga de presupuesto → P2.html
│   ├─ Carga / autoriza Mkt → P3.html
│   └─ Gerencia Admon&Fin.Mkt → HomeP1.html
│
├─ Tabla de solicitudes (folios F-260xx) → detalle por estado
│   ├─ F-26001 → PMktBorradorNormal.html        ✅
│   ├─ F-26002 → PMktBorradorBloqueado.html      ❌ inexistente
│   ├─ F-26003 → PMktBorradorPermitido.html      ❌ inexistente
│   ├─ F-26004 → PMktPendienteNormal.html        ✅
│   ├─ F-26005 → PMktPendienteExcedente.html     ❌ inexistente
│   ├─ F-26006 → PMktAjustesNormal.html          ✅
│   ├─ F-26007 → PMktAjustesExcedente.html       ❌ inexistente
│   ├─ F-26008 → PMktRechazada.html              ✅
│   ├─ F-26009 → PMktAprobada.html               ✅
│   ├─ F-26010 → PInverBorrador.html             ❌ inexistente
│   ├─ F-26011 → PInverPendiente.html            ❌ inexistente
│   ├─ F-26012 → PInverAjustes.html              ❌ inexistente
│   ├─ F-26013 → PInverRechazada.html            ❌ inexistente
│   └─ F-26014 → PInverAprobada.html             ❌ inexistente
│
├─ Botón "Nueva Solicitud" → modal #modalTipoSolicitud
│   ├─ Crear (Ordinario) → NuevaSol_Ordinario.html
│   └─ Crear (Inversión)  → NuevaSol_Inversion.html
│
├─ Botón "Descargar Reporte" → modal #modalReporteCarga
├─ Ícono fila (eliminar) → modal #modalConfirmarEliminacion
│
└─ Continuidad de flujo vía menú: SelGrupoEmpresarial → AEjercicio → (detalle/alta)
                                   → Autorizaciones → Liberaciones → SIPRES
```

### Cómo se llega a `AEjercicio.html`
- Desde `SelGrupoEmpresarial.html` se llega a sus **variantes con sufijo**
  (`AEjercicio_BackOffice.html`, `AEjercicio_GrupoElektra.html`, `AEjercicio_Totalplay.html`),
  no a `AEjercicio.html` "pelón".
- `AEjercicio.html` (sin sufijo) **solo recibe regresos** desde las pantallas de detalle
  `PMkt*` (botón volver). Es decir: como nodo raíz funciona, pero en la maqueta tal cual **no
  tiene una entrada directa desde el menú** — se entra por sus variantes de grupo.

---

## 3. Árbol detallado por pantalla (flujo que nace en `AEjercicio.html`)

> Se detallan la pantalla raíz y su flujo inmediato (E8). Para el resto de hubs alcanzables
> por el menú compartido (Parámetros, Forecast/Base, Autorizaciones, Liberaciones, Sistema),
> ver §3 de [`mapa-navegacion-maqueta.md`](./mapa-navegacion-maqueta.md).

## AEjercicio.html — Ejercicio de Carga Presupuestal (RAÍZ)

- Archivo: `AEjercicio.html`
- Módulo: `Planeación Presupuestal / Carga Presupuestal`
- Épica relacionada: `E8 (Carga presupuestal)`
- Acceso desde: regreso desde detalles `PMkt*`; sus variantes (`_BackOffice`, `_GrupoElektra`,
  `_Totalplay`) se acceden desde `SelGrupoEmpresarial.html`.
- Opciones de menú que llevan ahí: "Planeación Presupuestal → Carga Presupuestal"
  (`SelGrupoEmpresarial.html` → variantes de `AEjercicio`).
- Tipo de pantalla: `listado de solicitudes + tablero`

### Elementos de navegación detectados
- Breadcrumb: No
- Menú local (sidebar): Sí (menú maestro)
- Tabs: Sí (3)
- Acordeones: No
- Modales disparados desde esta pantalla: Sí (`#modalTipoSolicitud`, `#modalReporteCarga`,
  `#modalConfirmarEliminacion`, `#filtrosAvanzados`, `#filtrosAvanzadosResumen`)

### Acciones de navegación
| Elemento | Texto / ícono | Tipo | Destino actual | Destino esperado | Observaciones |
|---|---|---:|---|---|---|
| Botón | Nueva Solicitud | modal | `#modalTipoSolicitud` | selector tipo | OK |
| Link (en modal) | Crear (Ordinario) | link | `NuevaSol_Ordinario.html` | igual | correcto |
| Link (en modal) | Crear (Inversión) | link | `NuevaSol_Inversion.html` | igual | correcto |
| Botón | Descargar Reporte | modal | `#modalReporteCarga` | modal reporte | OK |
| Botón | Filtros Avanzados | modal | `#filtrosAvanzados` / `#filtrosAvanzadosResumen` | filtros | OK |
| Ícono fila | (eliminar) | modal | `#modalConfirmarEliminacion` | confirmación | OK |
| Sidebar local | Registro de Bases Presupuestales | link | `BPRegistros.html` | igual | correcto |
| Sidebar local | Reportes | link | `Reportes.html` | igual | correcto |
| Cards perfil | Carga de presupuesto / Mkt / Gerencia | link | `P2.html` / `P3.html` / `HomeP1.html` | igual | correcto |

### Tabla de la pantalla — Solicitudes de carga (folios F-260xx)
- Columnas relevantes: Folio, estado, importes, acciones.
- Acción por fila: link en el folio → pantalla de detalle según estado.

| Folio | Destino | ¿Existe? | Observaciones |
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
| F-26010..F-26014 | `PInverBorrador/Pendiente/Ajustes/Rechazada/Aprobada.html` | ❌ | **5 rotos** (Inversión sin pantallas) |

### Modales
- `#modalTipoSolicitud` — selector Ordinario/Inversión; sus botones "Crear" **sí navegan**
  (`NuevaSol_Ordinario.html` / `NuevaSol_Inversion.html`).
- `#modalReporteCarga` — descarga de reporte (sin navegación).
- `#modalConfirmarEliminacion` — confirmación por fila (sin navegación).

### Flujo representado
Núcleo de la **Carga Presupuestal (E8)**: bandeja de solicitudes del grupo, con estados de
gasto Mkt e Inversión, alta de nuevas solicitudes y descarga de reportes. Desde aquí el flujo
continúa (vía menú) a **Autorizaciones (E9)** y **Liberaciones (E10)**.

### Problemas detectados
- **9 de 14 estados rotos** (toda la rama de Inversión `PInver*` y los sufijos
  `Bloqueado/Permitido/Excedente`).
- `AEjercicio.html` "pelón" no tiene entrada directa de menú (se entra por las variantes de
  grupo) → como raíz aislada es alcanzable solo por regreso desde `PMkt*`.
- Posible duplicado: `AEjercicio.html` ≈ `AEjercicio_BackOffice/GrupoElektra/Totalplay`.

---

## AEjercicio_BackOffice / AEjercicio_GrupoElektra / AEjercicio_Totalplay — Variantes por grupo

- Módulo: `Carga Presupuestal` · Épica: `E8`
- Acceso desde: `SelGrupoEmpresarial.html` (cards de grupo empresarial).
- Tipo: igual que `AEjercicio.html` (bandeja de solicitudes), con datos del grupo.
- Mismos componentes y **mismos 9 estados rotos** por fila.
- `AEjercicio_GrupoElektra.html` añade un link extra roto: `ReportesCarga.html` (→ debería ser
  `Reportes.html`/`ReportesPPTO.html`).

---

## PMktBorradorNormal / PMktPendienteNormal / PMktAjustesNormal / PMktRechazada / PMktAprobada — Detalle de Solicitud

- Módulo: `Carga Presupuestal` · Épica: `E8` (+`E9` para Aprobada/Rechazada)
- Acceso desde: `AEjercicio*.html` (link de folio)
- Tipo: `detalle de solicitud` · Tabs (3) · Acordeones (11)
- Modales en estados editables (`PMktBorradorNormal`, `PMktAjustesNormal`).
- **Regreso:** vuelven a `AEjercicio.html` (no a la variante de grupo de origen) → incoherencia
  menor de continuidad.

### Problemas detectados
- Solo existen 5 de los 14 estados referenciados por la tabla raíz.
- Botón de regreso no respeta el grupo de origen.

---

## NuevaSol_Ordinario.html / NuevaSol_Inversion.html — Alta de Solicitud

- Módulo: `Carga Presupuestal` · Épica: `E8`
- Acceso desde: `AEjercicio*.html` (modal `#modalTipoSolicitud` → "Crear")
- Tipo: `formulario / wizard` · Acordeones (5) · Numerosos modales de validación/envío
  (`#modalValidacion`, `#modalQuitarCeco`, `#modalBorrador`, `#modalBorradorExito`,
  `#modalCancelar`, `#modalConfirmarEnvio`, `#modalEnvioBloqueado`, `#modalEnvio`;
  `#modalNuevoProyecto` en Inversión).

### Flujo representado
Captura de solicitud (ordinaria o de inversión), distribución por CeCo, guardar borrador y
enviar a autorización.

### Problemas detectados
- **Flujo truncado:** el modal de envío exitoso no enlaza a `Autorizaciones.html`; el paso
  "enviar → bandeja de autorización" no se completa por navegación.
- Placeholders de render JS (`${c.num}`/`${c.nombre}`) en disparadores de modal (sin efecto de
  negocio).

---

## Continuidad del flujo (hubs alcanzados por el menú)

Desde `AEjercicio.html`, vía menú lateral, el flujo de negocio continúa hacia:

- **SelGrupoEmpresarial.html** (paso previo: selección de grupo) — E8
- **Autorizaciones.html** → `AutorizacionN1/N2/N3`, `DetalleAprobada/Rechazada`,
  `AutorizacionExcedente/Remanente` — E9 / E12
- **Liberaciones.html** → modal "Exponer a SIPRES", tab Bitácora — E10
- **SIPRES.html** / **BPresupuestal.html** (Forecast y base) — E7
- **Parámetros / CeCos / GCuentas / CTransversal / PFondo / PUsuarios** (configuración) — E1/E6

> Cada uno de estos hubs está detallado en §3 del mapa de `index.html`
> ([`mapa-navegacion-maqueta.md`](./mapa-navegacion-maqueta.md)); no se duplica aquí.

---

## 4. Árbol por épica (desde la perspectiva de Carga)

La raíz `AEjercicio.html` pertenece a **E8** y es el centro del recorrido. El orden natural del
flujo de negocio visto desde aquí:

```
E1/E7 (config + base)  →  E8 (CARGA: AEjercicio)  →  E9 (Autorizaciones)  →  E10 (Liberación SIPRES)
        ▲                         │                                              
   E6 (usuarios/perfiles)   E12 (excedentes/remanentes, vía E9)                  
```

### Épica E8 — Carga Presupuestal  ⟵ **raíz aquí**
- Pantallas: `SelGrupoEmpresarial` → `AEjercicio(_BackOffice/_GrupoElektra/_Totalplay)` →
  `PMkt*` (5 existentes) / `NuevaSol_Ordinario` / `NuevaSol_Inversion`.
- Flujo alterno/duplicado: `ReportesPPTO` → `NuevaSol`, `NuevaCarga`, `VerSolicitud`,
  `AjusteSol`, `SolCorrecta`, `SolAprob`, `RechazarSol`, `EditarCarga`.
- Punto de entrada (esta vista): `AEjercicio.html`.
- Vacíos: 9/14 estados rotos; envío sin enlace a Autorizaciones; duplicidad `AEjercicio*` ⟷
  `ReportesPPTO`.

### Épicas E1, E6, E7, E9, E10, E12
Idénticas al mapa de `index.html`. Resumen de continuidad desde la Carga:
- **E9 Autorizaciones:** `Autorizaciones.html` → `AutorizacionN1/N2/N3`, `DetalleAprobada/Rechazada`. Regresos rotos a `BandejaAutorizaciones.html` (→ `Autorizaciones.html`).
- **E10 Liberación a SIPRES:** `Liberaciones.html` (tabs aprobadas/pendientes/SIPRES/bitácora) → modal `#modalLiberar`.
- **E12 Ajustes especiales:** `AutorizacionExcedente(2)` / `AutorizacionRemanente` / `AjusteSol`.
- **E7 Forecast/Base:** `SIPRES → ForecastDetalle`; `BPresupuestal → BPCalculada → BPV1`; `BPRegistros → BPCerrada`.
- **E1 Parámetros/Catálogos:** `Parametros`, `CeCos`, `GCuentas`, `CTransversal`, `PFondo`.
- **E6 Usuarios:** `PUsuarios → DetalleUsuario → EditarUsuario/DuplicarUsuario` (`NewUser` vacío).

> Detalle completo por épica en §4 de [`mapa-navegacion-maqueta.md`](./mapa-navegacion-maqueta.md).

---

## 5. Archivos huérfanos

El conjunto de huérfanos es **el mismo** que en el mapa de `index.html` (41 pantallas de
negocio), porque `AEjercicio.html` e `index.html` pertenecen al mismo componente conexo.
Tabla completa en §5 de [`mapa-navegacion-maqueta.md`](./mapa-navegacion-maqueta.md).

Resumen: cluster `Sketch*` (~21), borradores `posibleParametrosViejos (1..5)`, variantes de
Forecast (`ForecastActivo`, `ForecastActivo22`, `ForecastPresupuestal`, `EditForecast`,
`NuevoForecast`), `RevisarAu`, `NGCuenta`, `DetalleCecoBase`, `PUsuarios-Detalle`,
`CTransversalHU3/HU4`, `SIPRES2`, `BPresupuestal.html.html`, `ParametrosViejos20`,
`Parametrosversion2`, `SketchVerParametros`.

**Huérfanos especialmente relevantes para el flujo de Carga (E8):**
- Los **9 estados faltantes** referenciados por `AEjercicio*` no son huérfanos: **no existen**
  (ver §6). Si se decide crearlos, encajarían como detalles colgando de `AEjercicio*`.

---

## 6. Links rotos o inconsistentes (originados en `AEjercicio*` + globales)

### Rotos que nacen en la raíz y sus variantes
| Archivo origen | Elemento | Texto | Link actual | Link sugerido | Tipo | Comentario |
|---|---|---|---|---|---|---|
| `AEjercicio*.html` | link tabla | F-26002 | `PMktBorradorBloqueado.html` | crear o reasignar a estado existente | archivo inexistente | 8 inst. |
| `AEjercicio*.html` | link tabla | F-26003 | `PMktBorradorPermitido.html` | crear o reasignar | archivo inexistente | 8 inst. |
| `AEjercicio*.html` | link tabla | F-26005 | `PMktPendienteExcedente.html` | crear o reasignar | archivo inexistente | 8 inst. |
| `AEjercicio*.html` | link tabla | F-26007 | `PMktAjustesExcedente.html` | crear o reasignar | archivo inexistente | 8 inst. |
| `AEjercicio*.html` | link tabla | F-26010 | `PInverBorrador.html` | crear pantalla de inversión | archivo inexistente | 8 inst. |
| `AEjercicio*.html` | link tabla | F-26011 | `PInverPendiente.html` | crear | archivo inexistente | 8 inst. |
| `AEjercicio*.html` | link tabla | F-26012 | `PInverAjustes.html` | crear | archivo inexistente | 8 inst. |
| `AEjercicio*.html` | link tabla | F-26013 | `PInverRechazada.html` | crear | archivo inexistente | 8 inst. |
| `AEjercicio*.html` | link tabla | F-26014 | `PInverAprobada.html` | crear | archivo inexistente | 8 inst. |
| `AEjercicio_GrupoElektra.html` | link | (reporte) | `ReportesCarga.html` | `Reportes.html` / `ReportesPPTO.html` | archivo inexistente | 1 inst. |
| `NuevaSol_Ordinario/Inversion.html` | modal envío | Enviar | (modal terminal) | `Autorizaciones.html` | flujo incompleto | continuidad E8→E9 |

### Rotos globales que afectan la continuidad del flujo de Carga
| Archivo origen | Texto | Link actual | Link sugerido | Tipo |
|---|---|---|---|---|
| `AutorizacionN1/N2/N3.html`, `DetalleAprobada.html` | Volver | `BandejaAutorizaciones.html` | `Autorizaciones.html` | archivo inexistente (19 inst.) |
| menú maestro | Registro de Bases Presupuestales | `javascript:;` | `BPRegistros.html` | acción sin destino |
| menú maestro | Movimientos Presupuestales | `" SCarga.html"` | `SCarga.html` | naming (espacio inicial) |
| `SCarga.html`/`Modulos.html` | Forecast | `Forecast.html` | `SIPRES.html` | archivo inexistente |

> Tabla consolidada completa (incluye usuarios, parámetros, typos, etc.) en §6 de
> [`mapa-navegacion-maqueta.md`](./mapa-navegacion-maqueta.md).

---

## 7. Recomendaciones de corrección (prioridad para el flujo de Carga)

### Prioridad alta
1. **`AEjercicio.html` + 3 variantes** — resolver los **9 estados rotos** de la tabla de
   folios: decidir con negocio si se crean las pantallas faltantes
   (`PMkt*Bloqueado/Permitido/Excedente`, `PInver*`) o si los folios se reapuntan a los 5
   detalles existentes. **Es la corrección de mayor impacto del sistema.**
2. **Cerrar E8→E9** — en `NuevaSol_Ordinario.html`/`NuevaSol_Inversion.html`, que el modal de
   envío exitoso enlace a `Autorizaciones.html`.
3. **Regreso de autorizaciones** — `BandejaAutorizaciones.html` → `Autorizaciones.html`.
4. **Menú maestro** — "Registro de Bases Presupuestales" → `BPRegistros.html`; corregir
   `" SCarga.html"`.
5. **`AEjercicio_GrupoElektra.html`** — `ReportesCarga.html` → `Reportes.html`/`ReportesPPTO.html`.

### Prioridad media
6. Definir con negocio si la bandeja oficial de Carga es `AEjercicio*` o `ReportesPPTO`
   (duplicidad de flujo) y deprecar la otra.
7. Homologar el botón "Volver" de los detalles `PMkt*` para regresar a la **variante de grupo
   de origen** (`AEjercicio_BackOffice/GrupoElektra/Totalplay`), no al `AEjercicio.html` pelón.
8. Dar a `AEjercicio.html` una entrada directa de menú (o consolidarlo con las variantes de
   grupo para eliminar el duplicado base).

### Prioridad baja
9. Limpiar placeholders de render JS (`${c.num}`) en disparadores de modal.
10. Resto de homologaciones globales (breadcrumbs, regresos a `Inicio.html`, typos): ver §7 de
    [`mapa-navegacion-maqueta.md`](./mapa-navegacion-maqueta.md).

---

### Anexo — Metodología
Misma que el mapa de `index.html`: BFS sobre el grafo de `href` de los 183 `.html` de
`main-files/roksyn/`, con nodo raíz `AEjercicio.html`, sin atravesar páginas demo de
plantilla. El alcance resultante (68 pantallas) coincide con el de `index.html` por tratarse
del mismo componente conexo; este documento reencuadra el análisis alrededor del flujo de
Carga Presupuestal (E8).
