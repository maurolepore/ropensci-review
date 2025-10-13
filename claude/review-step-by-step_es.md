# Revisión por Pares de Software de rOpenSci: Proceso Paso a Paso

## Roles Principales

1. **[Autor/a](https://devguide.ropensci.org/es/softwarereview_author.es.html)** - Persona que crea y envía el paquete
2. **[Editor/a](https://devguide.ropensci.org/es/softwarereview_editor.es.html)** - Gestiona el proceso de revisión de un paquete específico
3. **Líder Editorial (LE)** - Asigna editores/as a los envíos, maneja preguntas de alcance
4. **[Revisores/as](https://devguide.ropensci.org/es/softwarereview_reviewer.es.html)** (2 por paquete) - Voluntarios/as que revisan el paquete
5. **Bot** (@ropensci-review-bot) - Sistema automatizado que ejecuta verificaciones y gestiona el flujo de trabajo
6. **Gerente de Comunidad** - Invita a los participantes a la comunidad de Slack

## Proceso Paso a Paso

### Fase 1: Consulta Previa al Envío (Opcional)
1. **Autor/a** considera si su paquete está suficientemente maduro y [dentro del alcance](https://devguide.ropensci.org/es/softwarereview_policies.es.html#package-categories)
2. **Autor/a** puede abrir un [issue de consulta previa al envío](https://github.com/ropensci/software-review/issues/new/choose) para preguntar a los editores si el paquete está dentro del alcance
3. **LE** o **Editor/a** responde sobre el ajuste al alcance

### Fase 2: Envío
1. **Autor/a** crea un [nuevo issue](https://github.com/ropensci/software-review/issues/new/choose) en el repositorio `ropensci/software-review` usando la plantilla de envío
2. **Bot** automáticamente:
   - Publica mensaje de bienvenida con comando de ayuda
   - Ejecuta análisis comprensivo de [`pkgcheck`](https://docs.ropensci.org/pkgcheck/)
   - Publica reporte detallado incluyendo:
     - Análisis de dependencias del paquete
     - Propiedades estadísticas y percentiles
     - Visualización interactiva de red de llamadas entre funciones
     - Resultados de goodpractice
     - Resultados de R CMD check
     - Análisis de cobertura de pruebas
     - Verificaciones de complejidad ciclomática
     - Resultados de lintr
     - Resumen de "Instrucciones para Editor en Jefe"
3. **LE** revisa el envío y el reporte del bot
4. **LE** evalúa si el paquete está dentro del alcance
5. **LE** puede discutir el alcance con el equipo editorial en Slack si no está claro
6. Si está fuera del alcance, **LE** responde explicando por qué y cierra el issue
7. Si está dentro del alcance, **LE** asigna un **Editor/a** con el comando: `@ropensci-review-bot assign @username as editor`
8. **Bot** confirma la asignación y añade la etiqueta `1/editor-checks`

### Fase 3: Verificación Inicial del Editor/a (~1-2 semanas)
1. **Editor/a** usa la [**plantilla de editor**](https://devguide.ropensci.org/es/editortemplate.es.html) como lista de verificación
2. **Editor/a** revisa el reporte automático de pkgcheck en detalle
3. **Editor/a** verifica si el paquete cumple con los criterios mínimos y el alcance
4. **Editor/a** puede solicitar cambios antes de buscar revisores
5. Si el paquete no pasa las verificaciones, **Editor/a** pide a **Autor/a** que corrija los problemas
6. **Autor/a** hace las correcciones y **Editor/a** (o cualquiera) puede volver a ejecutar las verificaciones con: `@ropensci-review-bot check package`
7. **Editor/a** publica su evaluación editorial usando la plantilla de editor
8. **Gerente de Comunidad** invita a **Editor/a** y **Autor/a** al Slack de rOpenSci

### Fase 4: Búsqueda de Revisores/as (~2 semanas)
1. **Editor/a** pide a **Autor/a** que sugiera 3 revisores/as potenciales (puede usar 0-1 de ellos)
2. **Editor/a** busca 2 revisores/as de:
   - Base de datos de revisores/as voluntarios/as
   - Autores/as de dependencias del paquete o paquetes dependientes
   - Personas activas en dominios relevantes
   - Sugerencias del autor/a (usar con moderación)
3. **Editor/a** contacta a revisores/as potenciales (vía email o GitHub)
4. **Editor/a** usa la [plantilla de solicitud de revisión](https://devguide.ropensci.org/es/reviewrequesttemplate.es.html)
5. **Revisores/as potenciales** verifican [conflictos de interés](https://devguide.ropensci.org/es/softwarereview_policies.es.html#coi) usando la guía de COI
6. **Revisores/as** aceptan o declinan en unos días
7. **Editor/a** asigna revisores/as con: `@ropensci-review-bot assign @username as reviewer`
8. **Bot** automáticamente:
   - Añade al revisor/a a la lista de revisores/as
   - Establece fecha límite (típicamente 3 semanas)
   - Publica mensaje de bienvenida con enlace a la [guía de revisores/as](https://devguide.ropensci.org/es/softwarereview_reviewer.es.html)
   - Pide al revisor/a que complete el formulario de revisores/as (Airtable)
   - Actualiza etiquetas del issue cuando se asignan 2 revisores/as
9. **Editor/a** puede modificar fechas límite con: `@ropensci-review-bot set due date for @username to YYYY-MM-DD`
10. **Gerente de Comunidad** invita a **Revisores/as** al Slack de rOpenSci

### Fase 5: Revisión (~2-3 semanas por revisor/a)
1. **Revisores/as** examinan el paquete independientemente
2. **Revisores/as** usan la [**plantilla de revisión**](https://devguide.ropensci.org/es/reviewtemplate.es.html) como lista de verificación
3. **Revisores/as** verifican:
   - Calidad y estilo del código
   - Completitud de la documentación
   - Cobertura de pruebas
   - Usabilidad y diseño de API
   - Cumplimiento con [estándares de empaquetado de rOpenSci](https://devguide.ropensci.org/es/pkg_building.es.html)
4. **Bot** envía recordatorio cuando se acerca la fecha límite (ej., "quedan 2 días")
5. **Revisores/as** publican sus revisiones como comentarios en el issue de GitHub
6. **Editor/a** registra cada revisión con: `@ropensci-review-bot submit review <url> time <hours>`
7. **Bot** registra las horas de revisión de cada revisor/a
8. **Revisores/as** pueden hacer pull requests con correcciones (opcional, ~20% lo hace)

### Fase 6: Respuesta del Autor/a (~2-3 semanas)
1. **Autor/a** lee ambas revisiones
2. **Autor/a** responde a cada punto planteado
3. **Autor/a** hace cambios al paquete
4. **Autor/a** explica decisiones si no implementa sugerencias (diálogo, no órdenes)
5. **Autor/a** sube actualizaciones a GitHub
6. **Autor/a** comenta en el issue cuando esté listo/a para re-revisión

### Fase 7: Iteración (Variable)
1. **Revisores/as** verifican las respuestas y actualizaciones del autor/a
2. **Revisores/as** pueden solicitar cambios adicionales
3. **Autor/a** hace más actualizaciones
4. **Proceso se repite** hasta que los revisores/as estén satisfechos/as
5. **Sin rechazo** - el proceso continúa hasta que el paquete cumpla con los estándares

### Fase 8: Aprobación
1. **Revisores/as** usan la [plantilla de aprobación](https://devguide.ropensci.org/es/approval2template.es.html) para aprobar formalmente
2. **Revisores/as** publican comentarios de aprobación
3. **Editor/a** confirma que todos los problemas han sido abordados
4. **Editor/a** ejecuta la aprobación final con: `@ropensci-review-bot approve <nombre-paquete>`
5. **Bot** automáticamente publica lista comprensiva de TAREAS PENDIENTES para el autor incluyendo:
   - Instrucciones de transferencia del repositorio
   - Comando de finalización post-transferencia
   - Instrucciones para corregir enlaces
   - Eliminación del archivo de código de conducta
   - Opciones de migración del sitio web pkgdown
   - Actualizaciones de badges
   - Instrucciones de incremento de versión
   - Generación de [Codemeta](https://codemeta.github.io/)
   - Instrucciones de instalación de [R-universe](https://ropensci.org/r-universe/)
   - Instrucciones de reconocimiento a revisores/as
   - Invitación a blog post
   - Enlaces a guías post-incorporación
6. **Bot** envía invitación de transferencia del repositorio al autor
7. **Paquete es aceptado** en rOpenSci

### Fase 9: Post-Aceptación - Transferencia del Repositorio
1. **Autor/a** debe habilitar autenticación de dos factores (2FA) en su cuenta de GitHub
2. Invitación del **Bot** expira después de 1 semana (puede renovar con: `@ropensci-review-bot invite me to ropensci/<nombre-paquete>`)
3. **Autor/a** transfiere el repositorio a la organización `ropensci` vía Configuración de GitHub
4. **Autor/a** notifica al bot con: `@ropensci-review-bot finalize transfer of <nombre-paquete>`
5. **Bot** completa la transferencia:
   - Hace al equipo `<nombre-paquete>` propietario del repositorio
   - Invita al autor al equipo
   - Restaura acceso de administrador al autor

### Fase 10: Post-Aceptación - Finalización
1. **Autor/a** completa la lista de verificación de TAREAS PENDIENTES:
   - [x] Corregir todos los enlaces para que apunten a la organización ropensci
   - [x] Eliminar archivo CODE_OF_CONDUCT existente ([aplica el de rOpenSci](https://ropensci.org/code-of-conduct/))
   - [x] Decidir sobre el sitio web pkgdown (mantener propio o migrar a docs.ropensci.org)
   - [x] Actualizar badges de CI/cobertura a las nuevas URLs
   - [x] Incrementar la versión del paquete
   - [x] Actualizar NEWS.md con cambios realizados durante la revisión
   - [x] Ejecutar [`codemetar::write_codemeta()`](https://docs.ropensci.org/codemetar/) para generar [codemeta.json](https://codemeta.github.io/)
   - [x] Añadir instrucciones de instalación de [R-universe](https://ropensci.org/r-universe/) al README
   - [ ] Opcionalmente reconocer a revisores/as como "rev" en DESCRIPTION
2. **Editor/a** puede etiquetar a editores de blog sugiriendo un [blog post](https://blogguide.ropensci.org/)
3. **Editor/a** añade el paquete a la documentación de rOpenSci
4. **Editor/a** cierra el issue de revisión
5. **Paquete aparece** en el sitio web de rOpenSci
6. **Opcional**: Autor/a puede enviar a [Journal of Open Source Software](https://joss.theoj.org/) (vía rápida)
7. **Opcional**: Autor/a envía a CRAN/Bioconductor
8. **Autor/a** revisa guías post-incorporación:
   - [Guía de colaboración](https://devguide.ropensci.org/es/maintenance_collaboration.es.html)
   - [Guía de publicaciones](https://devguide.ropensci.org/es/maintenance_releases.es.html)
   - [Guía de marketing](https://devguide.ropensci.org/es/maintenance_marketing.es.html)

## Características Clave

- **Cronograma**: Típicamente 2-3 meses en total (mínimo ~5-6 semanas)
- **Público y Transparente**: Todo sucede en issues públicos de GitHub
- **Iterativo**: No es de una sola vez como la revisión académica por pares
- **Sin rechazo**: El proceso continúa hasta que el paquete cumple con los estándares
- **Colaborativo**: Autores/as y revisores/as participan en diálogo
- **Altamente Automatizado**: El bot maneja verificaciones, recordatorios, asignaciones, registro y transferencia
- **Dirigido por Voluntarios/as**: Editores/as y revisores/as son voluntarios/as no remunerados/as
- **Enfocado en Comunidad**: Invitaciones a Slack para todos los participantes

## La Comunicación Ocurre Vía:
- **Hilo del issue de GitHub** (comunicación principal)
- **Comandos del bot** (automatización del flujo de trabajo)
- **Slack** (conexión comunitaria y discusiones internas del equipo editorial)
- **Email** (reclutamiento de revisores/as)

## Referencia de Comandos del Bot

Documentación completa: [Guía de Comandos del Bot](https://devguide.ropensci.org/es/bot_cheatsheet.es.html)

| Comando | Quién lo Usa | Propósito |
|---------|--------------|-----------|
| `@ropensci-review-bot help` | Cualquiera | Obtener ayuda con comandos del bot |
| `@ropensci-review-bot check package` | Cualquiera | Re-ejecutar pkgcheck automatizado |
| `@ropensci-review-bot assign @username as editor` | LE | Asignar editor al envío |
| `@ropensci-review-bot assign @username as reviewer` | Editor/a | Asignar revisor/a (establece fecha límite automáticamente) |
| `@ropensci-review-bot set due date for @username to YYYY-MM-DD` | Editor/a | Cambiar fecha límite del revisor/a |
| `@ropensci-review-bot submit review <url> time <hours>` | Editor/a | Registrar revisión con horas dedicadas |
| `@ropensci-review-bot approve <paquete>` | Editor/a | Aprobar paquete y publicar lista de TAREAS |
| `@ropensci-review-bot invite me to ropensci/<paquete>` | Autor/a | Renovar invitación de transferencia expirada |
| `@ropensci-review-bot finalize transfer of <paquete>` | Autor/a | Completar transferencia del repositorio |

## Plantillas Clave Usadas:
- [**Plantilla de envío**](https://github.com/ropensci/software-review/issues/new/choose) - Usada por autores/as al crear el issue
- [**Plantilla de editor/a**](https://devguide.ropensci.org/es/editortemplate.es.html) - Usada por editores/as para verificaciones iniciales
- [**Plantilla de solicitud de revisión**](https://devguide.ropensci.org/es/reviewrequesttemplate.es.html) - Usada por editores/as para invitar revisores/as
- [**Plantilla de revisión**](https://devguide.ropensci.org/es/reviewtemplate.es.html) - Usada por revisores/as para realizar su revisión
- [**Plantilla de aprobación**](https://devguide.ropensci.org/es/approval2template.es.html) - Usada por revisores/as para aprobar formalmente
- **Comentario de aprobación del editor/a** - Usado por editores/as para aprobación final del paquete

## Características Automatizadas del Bot

### Al Enviar:
- Mensaje de bienvenida
- Reporte comprensivo de pkgcheck
- Análisis estadístico y visualizaciones

### Durante la Revisión:
- Confirmaciones de asignación
- Recordatorios de fechas límite
- Solicitudes de formulario de revisores/as
- Gestión de etiquetas

### Al Aprobar:
- Generación de lista comprensiva de TAREAS PENDIENTES
- Invitación de transferencia del repositorio
- Finalización de transferencia
- Restauración de acceso de administrador

### Durante Todo el Proceso:
- Puede re-ejecutar verificaciones bajo demanda
- Registra horas de revisión
- Gestiona el estado del flujo de trabajo
