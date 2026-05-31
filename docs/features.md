# Features implementadas — Sistema de Gestión Elared

## Base (app original)
- Login con usuario/contraseña (admin hardcodeado + supervisores en Firestore)
- CRUD de tareas (crear, editar, eliminar, restaurar desde papelera)
- Vista Lista y Kanban
- Filtros: supervisor, estado, prioridad, vencidas
- Búsqueda global (incluyendo comentarios)
- Comentarios en tareas
- Historial de cambios por tarea
- Archivos adjuntos (base64 en Firestore)
- Papelera de reciclaje (30 días)
- Solicitudes de supervisores al admin
- Notificaciones internas
- Dashboard con 4 gráficos (Chart.js)
- Calendario mensual de tareas
- Actividad del equipo (log)
- Mi panel (stats por supervisor)
- Sesiones activas
- Exportar tareas a Excel y PDF
- Modo oscuro y temas de color
- Buscador global con índice de comentarios
- Inactividad automática (30 min)

## 33 features nuevas

| # | Feature | Descripción |
|---|---------|-------------|
| 1 | Doble verificación al eliminar | Modal que pide escribir "ELIMINAR". Reemplaza todos los `confirm()` del browser |
| 2 | Export productividad PDF | Botón en Dashboard → PDF con stats por supervisor + comparativa mensual |
| 3 | Export productividad Excel | Botón en Dashboard → Excel con mismos datos |
| 4 | Comparativa entre períodos | Cards de productividad muestran este mes vs mes anterior con flechas ↑↓ |
| 5 | Drag & Drop en Kanban | Tarjetas arrastrables entre columnas; actualiza estado en Firebase al soltar |
| 6 | Vista compacta | Toggle "Compacto" en toolbar; oculta descripción y metadata secundaria |
| 7 | Tamaño de texto ajustable | En Admin: botones Pequeño/Normal/Grande (12/14/16px). Persiste en localStorage |
| 8 | Subtareas con checklist | Nueva pestaña en modal. Agregar/marcar/eliminar. Barra de progreso. Firestore subcolección `subtareas` |
| 9 | Plantillas de tareas | "Guardar como plantilla" en formulario. Sección en Admin para gestionar y usar plantillas |
| 10 | Tiempo estimado vs real | Campos `horasEst` y `horasReal` en modal. Se muestra en cards de productividad |
| 11 | Etiquetas y categorías | Campo `tags` al crear/editar. Chips de color en tarjetas. Filtro por etiqueta en toolbar |
| 12 | Duplicar tarea | Botón ⊕ en cada tarjeta y en modal. Crea copia con prefijo "[Copia]" |
| 13 | Porcentaje de avance | Slider 0-100% en modal. Barra de progreso en tarjeta. Supervisor puede actualizar |
| 14 | Prioridad automática 48h | Borde naranja parpadeante si tarea vence en menos de 48hs |
| 15 | Tareas recurrentes | Checkbox + frecuencia. Al terminar, crea automáticamente la siguiente instancia |
| 16 | Archivado automático | Tareas terminadas hace +30 días → colección `tareas_archivadas`. Se ejecuta al cargar |
| 17 | Ranking de supervisores | En Dashboard: ranking del mes por % cumplimiento con medallas 🥇🥈🥉 |
| 18 | Reporte de vencidas | Tabla en Dashboard: tareas vencidas sin completar, supervisor, días de retraso |
| 19 | Foto de perfil | Upload en "Editar usuario". Base64 ≤1MB. Se muestra en avatar del header |
| 20 | Suspender usuario | Botón en Admin. Suspendido no puede hacer login. Badge visual |
| 21 | Menciones @ en comentarios | Al escribir @ aparece dropdown con supervisores. Mención resaltada en azul. Notificación interna |
| 22 | Email al cambiar estado | Cuando admin cambia estado → email al supervisor via EmailJS |
| 23 | Reacciones en comentarios | Botones 👍 ✅ ⚠ bajo cada comentario. Toggle propio. Contador. Firestore |
| 24 | Gráfico Burndown | Línea con tareas pendientes por día en últimos 30 días |
| 25 | Historial de logins | En Admin: tabla con últimos 20 accesos (usuario, fecha, dispositivo, navegador) |
| 26 | Bloquear tarea | Campo "bloqueada por" en modal. Badge 🔒. No permite marcar terminada hasta desbloquear |
| 27 | Dashboard exportable a PDF | Captura los 4 gráficos (canvas.toDataURL) + tabla resumen → PDF landscape |
| 28 | Clonar semana | En Admin: duplica todas las tareas de los últimos 7 días con estado=pendiente y fechas+7 |
| 29 | Recuperación de contraseña | Link en login → modal → busca por usuario en Firestore → envía contraseña temporal via EmailJS |
| 30 | Comparativa mensual en reportes | PDF y Excel de productividad incluyen columnas de variación % vs mes anterior |
| 31 | Vista calendario mejorada | Clic en día abre panel lateral con todas sus tareas. Indicador urgente |
| 32 | Notificación sonora | Toggle en Admin. Web Audio API: beep al recibir notificaciones internas |
| 33 | Modo compacto en Kanban | El toggle Compacto también aplica al kanban (oculta metadata de tarjetas) |

## Colecciones Firestore

```
tareas/              → tareas principales
  {id}/comentarios/  → comentarios con reacciones
  {id}/historial/    → historial de cambios
  {id}/subtareas/    → subtareas (F8)
  {id}/archivos/     → adjuntos base64
usuarios/            → supervisores
solicitudes/         → solicitudes de supervisores
notif/{uid}/items/   → notificaciones internas
actividad/           → log de actividad del equipo
sesiones/            → sesiones activas (heartbeat 5min)
loginHistorial/      → historial de logins (F25)
papelera/            → tareas eliminadas (30 días)
tareas_archivadas/   → tareas terminadas +30 días (F16)
plantillas/          → plantillas de tareas (F9)
```
