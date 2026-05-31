# Sistema de Gestión de Tareas — Elared

App web single-file para gestión de tareas del equipo VOS Agente Oficial ANTEL. Corre completamente en el browser, sin servidor backend. Datos en Firebase Firestore en tiempo real.

## Demo

🌐 **URL de producción:** https://tareas-elared.netlify.app

---

## Acceso

| Rol | Usuario | Contraseña |
|-----|---------|------------|
| Administrador | `admin` | `Elared2024` |
| Supervisor | (ver panel Admin) | (definida al crear el usuario) |

> El admin ve todo y gestiona supervisores. Los supervisores ven solo sus tareas.

---

## Configuración de Firebase

**Project ID:** `elared-3789d`

Para conectar una instancia nueva, al abrir la app sin configuración previa aparece la pantalla de setup. Pegá el `firebaseConfig` de la consola de Firebase:

```js
{
  apiKey: "...",
  authDomain: "elared-3789d.firebaseapp.com",
  projectId: "elared-3789d",
  storageBucket: "elared-3789d.appspot.com",
  messagingSenderId: "...",
  appId: "..."
}
```

La configuración se guarda en `localStorage` bajo la clave `fb_config_v1`.

---

## Configuración de EmailJS

Se usa para notificar supervisores cuando se les asigna/cambia una tarea, y para recuperación de contraseña.

| Parámetro | Valor |
|-----------|-------|
| Service ID | `service_h8k23dj` |
| Template ID | `template_ra59p96` |
| Public Key | `AHd1FcXhc41yHthRs` |

El supervisor debe tener un email registrado en Admin → Editar usuario.

---

## Deploy en Netlify

### Opción A: Deploy automático desde GitHub (recomendado)

1. Conectar este repositorio a Netlify:
   - Netlify Dashboard → Add new site → Import from Git
   - Seleccionar `isaacondon-commits/elared-sistema-gestion`
   - Branch: `main`
   - Publish directory: `/` (raíz)
2. Cada push a `main` dispara deploy automático.

### Opción B: Deploy manual (Netlify Drop)

```bash
netlify deploy --prod --dir . --site tareas-elared
```

---

## Cómo agregar supervisores

1. Ir a Admin → "Agregar usuario"
2. Completar: nombre completo, usuario (para login), contraseña, email
3. El supervisor puede hacer login inmediatamente
4. Para editar o suspender: Admin → botón "Editar" o "Suspender"

---

## Cómo actualizar la app

El sistema es un single-file HTML (`index.html`). Para actualizar:

```bash
# Editar index.html con los cambios
git add index.html
git commit -m "feat: descripción del cambio"
git push origin main
# Netlify despliega automáticamente en ~30 segundos
```

---

## Estructura del proyecto

```
elared-sistema-gestion/
├── index.html          ← App completa (single-file)
├── README.md           ← Este archivo
├── backups/            ← Copias de seguridad por fecha
│   └── tareas_backup_YYYYMMDD.html
└── docs/
    └── features.md     ← Lista completa de features
```

---

## Features incluidas

Ver [docs/features.md](docs/features.md) para la lista completa de 33+ features.

Highlights:
- 📊 Dashboard con 4 gráficos + Burndown + Ranking
- 🗂 Vista Lista y Kanban con Drag & Drop
- ✅ Subtareas con checklist y progreso
- 🏷 Etiquetas y filtros avanzados
- 📎 Archivos adjuntos (base64)
- 🔒 Bloqueo de tareas entre dependencias
- 🔁 Tareas recurrentes automáticas
- 📧 Notificaciones por email (EmailJS)
- 📄 Export PDF y Excel (tareas + productividad + dashboard)
- 🌙 Modo oscuro + 6 temas de color
- 🔍 Búsqueda global (tareas + comentarios)
- 📱 Responsive

---

## Stack técnico

- **Frontend:** HTML + CSS + JavaScript vanilla (sin frameworks)
- **Base de datos:** Firebase Firestore (realtime)
- **Hosting:** Netlify
- **Librerías CDN:**
  - Firebase 10.12.0
  - Chart.js 4.4.0
  - jsPDF 2.5.1
  - SheetJS (XLSX) 0.18.5
  - EmailJS 4.x

---

*Desarrollado para VOS Agente Oficial ANTEL — Elared*
