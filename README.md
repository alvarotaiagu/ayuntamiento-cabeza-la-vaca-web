# Ayuntamiento de Cabeza la Vaca · propuesta de web «Puerta abierta» (v3)

Maqueta de la web municipal del **Ayuntamiento de Cabeza la Vaca** (Badajoz, 1.257 habitantes, INE 2025), hecha con la plantilla «Puerta abierta» v3 (`plantilla-ayuntamiento-puerta-abierta-web`) y con sus datos reales. Se le propone por correo.

- **No es la web oficial.** Lleva en todas las páginas la banda «Propuesta de diseño… no es la web oficial» y `noindex, nofollow`.
- Con `?revision` sale el mando de versión y color.
- Las fuentes de cada dato, el inventario de su web actual y sus errores están **fuera de esta carpeta**, en `../ayuntamiento-cabeza-la-vaca-bocetos/`: `DATOS.md`, `INVENTARIO.md` y `ERRORES.md`.
- **Solo en castellano**: no hay traducciones de «El pueblo» (decisión del 5-10-2026).

```bash
npm install                     # Playwright y axe-core (solo para los scripts)
node scripts/aplicar.mjs        # genera la web desde municipio.json, marca/, contenido/ y media/
node scripts/servir.mjs         # http://127.0.0.1:4192/  ·  con ?revision, el mando
node scripts/verificar.mjs      # todas las comprobaciones
```

`municipio.json` lo escribe `../ayuntamiento-cabeza-la-vaca-bocetos/_scripts/construir_municipio.py`; `contenido/avisos.json`, `agenda.json` y `noticias.json`, `construir_contenido.py`; los títulos claros del tablón, `tablon_claro.py`.

---

## El concepto

**La puerta del Ayuntamiento, abierta todo el día.** El arco de medio punto es el único motivo dibujado. El panel «Hoy en Cabeza la Vaca» dice tres cosas: si el Ayuntamiento está abierto (con la hora real), qué es lo próximo de la agenda y cuál es el último aviso.

Por qué le encaja a Cabeza la Vaca:
- **Publica mucho, pero fuera de la web.** El Ayuntamiento publica casi a diario en Bandomóvil («Cabeza la Vaca Informa», último comunicado el 1-10-2026), Instagram y Facebook, pero las noticias de su web están paradas desde el 28-05-2026. Aquí los avisos, la agenda y las noticias salen de ese canal, con su fecha y su fuente.
- **Su tablón oficial está en la sede de la Diputación** (20 documentos, el último del 2-10-2026) y su web no lo enseña: aquí entra solo y en lenguaje claro.
- **Tiene mucho que enseñar y lo tiene en imágenes.** El calendario de fiestas, las concejalías, el horario del Punto Limpio y el saludo del alcalde son fotos sin texto; aquí van en texto.
- **La castaña y el sello «Pueblo Mágico» están en «El pueblo»**: el castañar de Los Cortinales (unas 256 ha), la Feria de la Castaña (XXI edición, del 30 de octubre al 1 de noviembre de 2026, con su Pre-Feria), la ruta El Castañar, las castañas con leche, y la ficha del sello «Pueblos Mágicos de España» dicha con exactitud: lo concede una asociación privada por invitación, no la Junta.

**Marca: el azur del escudo.** El escudo tiene gules (21 %), oro (20 %), plata, sable, azur (14 %) y sinople (9 %). El oro nunca es marca (no llega a AA como texto); el gules es el color de las alertas; la plata y el sable no sirven. Queda el azur, que es el azul puro `#0000FF` del SVG de Commons y pasa AA tal cual. Si se prefiere un tono más amable, `python scripts/marca-desde-escudo.py --principal sinople --motivo "El castañar"`.

**Cortina: «El escudo a su sitio»** (`"cortina": "escudo"`), la de las otras webs. Solo en la portada y una vez por sesión, 1,2 s como mucho; se salta con un clic o una tecla; no existe con movimiento reducido y, sin GSAP, se quita sola. Depende del escudo, cuyo decreto de aprobación no consta; `"cortina": "puerta"` vuelve a la del arco.

## Mapa de páginas

| Página | Qué tiene |
|---|---|
| `index.html` | «Hoy» con la torre de la iglesia en el arco (4 fotos al azar), plazos abiertos, 5 atajos, tablón con filtros, agenda y noticias, teléfonos, «El año en Cabeza la Vaca», cifras y «Conocer Cabeza la Vaca» |
| `tramites.html` | Buscador, momentos («Me vengo a vivir aquí», «Voy a hacer obra», «Busco empleo», «Tengo una empresa», «Ha pasado algo en mi calle»), 4 temas y los 15 trámites de la sede |
| `ayuntamiento.html` | Corporación (PSOE 5, Unidas por Cabeza la Vaca 2, PP 2), «quién se ocupa de qué», normativa (34 ordenanzas de su web y las aprobadas en 2026) |
| `avisos.html` | Bandomóvil, avisos y el tablón de la sede (15 anuncios) |
| `noticias.html`, `agenda.html` | 5 noticias y la agenda de la Pre-Feria y la Feria, más las fiestas de fecha fija |
| `telefonos.html` | Listín (112 y 062, consultorio, farmacia, colegio, Aula Mentor, Mancomunidad…) e instalaciones municipales |
| `pueblo.html` | Qué ver (8 lugares con foto), **Para visitar** (Feria de la Castaña, Pueblo Mágico, Oficina de Turismo, Centro de Interpretación), historia, patrimonio, fiestas, gastronomía, personajes, rutas (11), **Dónde comer y dormir** (35 negocios) y el mapa del término de OpenStreetMap |
| `incidencia.html`, `escribanos.html`, `facil.html`, `transparencia.html`, `propuesta.html` | Formularios por correo, lectura fácil (5 trámites + incidencias), transparencia y la página para el alcalde |

## Lo de la v3 en este municipio

- `ine` 06024, `cifras` con su fuente, `incidencias`, `transparencia` (con enlaces solo comprobados), `propuesta_web` (5 problemas comprobables y la captura real de su portada en `assets/web-actual.jpg`), `canal_avisos` (Bandomóvil) y `farmacias.oficial` (única farmacia: solo el buscador del Colegio).
- Plano del pie y mapa del término desde OpenStreetMap: el Ayuntamiento es el nodo `node/13698719404` y el término `relation/346216`. Overpass no indexaba áreas en el espejo disponible, así que el mapa se hizo por caja (`_scripts/termino_bbox.mjs`) y se comprobó con `out tags` cada lugar emparejado: salieron 7 de 12 (plaza de toros, Cruz del Rollo, Torre del Reloj, iglesia, Fuente de Abajo, Cruz de Tordoya y Fuente del Rollo) y se dejaron 5 (se quitaron la iglesia y la Cruz de Tordoya porque sus círculos se pisaban a 320 px). La copia filtrada está en `../ayuntamiento-cabeza-la-vaca-bocetos/_osm/termino-bbox-filtrado.json`.
- Fotos igualadas (`fotos-igualar.py`): 5 de Commons (con autor y licencia) y 7 de la web del Ayuntamiento, **solo para esta maqueta**.
- El perfil del pie (el dibujo del pueblo) queda genérico: dibujarlo desde fotos reales (RESKIN §6 bis) es un paso aparte.
- `sede.tablon_url` **no** se usa: el tablón vivo es el de la sede.

## Pendientes del Ayuntamiento

- Horario de atención (ahora «Ejemplo», de 9:00 a 14:00).
- Correo de incidencias y de «Escríbanos» (ahora, el general).
- Teléfono de la Policía Local; qué cuartel de la Guardia Civil les corresponde (solo sale el 062).
- Fecha y hora del próximo pleno, y si se graban.
- Horario actual del Punto Limpio (el de invierno salió de un cartel de marzo), de la Oficina de Turismo y de la biblioteca.
- Calendario de recogida de residuos (folletos de Heyzine, ilegibles).
- Decidir qué datos publicar de las 31 asociaciones (su web da el móvil de cada presidente) y si quieren la guía comercial completa (aquí solo lo de comer y dormir).
- Autorización para leer su tablón (`tablon_autorizado`) y para usar las fotos de su web.
- Decreto del escudo y resolución de la Fiesta de Interés Turístico (no constan).
- `hoja.id` (la hoja de Google para publicar desde el móvil); fechas de los plazos de natalidad e IAE.
- `propuesta.html`: el `[PRECIO]` lo pone Álvaro.
- Que cambien la contraseña de la plataforma fotovoltaica que su web publica en abierto.

## Tablón: dos anuncios quitados a mano

El filtro de la plantilla deja pasar 2 documentos del tablón de la sede que parecen listas de personas («Acta Tribunal», 2024, y «Listado Ley del Jurado», 2025). `tablon_claro.py` los quita. Si algún día se activa la lectura automática, hay que añadir esos dos patrones a `scripts/lib/tablon.mjs` en la plantilla.
