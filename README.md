#  SIVIA - Sistema de Gestión de Accidentes de Tránsito
## Descripción
SIVIA es un sistema web diseñado para gestionar información relacionada con accidentes de tránsito.  
Permite administrar conductores, vehículos, víctimas, usuarios, condiciones viales, infraestructura, factores de riesgo, operativos, reportes policiales y seguros.  
Además, genera estadísticas gráficas con **Chart.js** para visualizar tendencias y patrones.
---
##  Tecnologías utilizadas
- **Frontend**: HTML, CSS, JavaScript
- **Backend**: Node.js + Express
- **Base de datos**: MongoDB
- **Gráficos**: Chart.js
- **Autenticación**: Tokens almacenados en `localStorage`
---
##  1. Autenticación
- **Login.html** → Página inicial de acceso.
- **Verificación de token**:
  - Si no existe token en `localStorage` Redirige a `login.html`.
  - Si existe token → Acceso al sistema.
- **Logout** Elimina token y redirige al login.
---
##  2. CRUD de Entidades
Cada módulo sigue el mismo patrón:
- **Listar** `cargarX()` `GET /api/X`
- **Editar** `editarX(id)` `GET /api/X/:id`
- **Eliminar** `eliminarX(id)` `DELETE /api/X/:id`
- **Crear/Actualizar** Formularios con `POST /api/X` o `PUT /api/X/:id`

### Entidades principales:
- Conductores
- Vehículos
- Víctimas
- Usuarios del sistema
- Accidentes
- Condiciones viales
- Infraestructura
- Factores de riesgo
- Operativos de tránsito
- Reportes policiales
- Seguros
---
##  3. Estadísticas
- **Accidentes por tipo** Gráfico de barras.
- **Factores de riesgo** Gráfico circular.
- Se generan con **Chart.js**.
- Se destruye el gráfico previo si ya existía para evitar duplicados.
---
##  4. Mensajes Globales
- **mostrarMensaje(texto, tipo)**:
  - Muestra alertas de éxito, error o advertencia.
  - Después de 4 segundos vuelve al mensaje por defecto:
    > "Sistema cargado correctamente. Asegúrate de que el backend esté ejecutándose para guardar y listar datos."
---
##  5. Formularios
- Cada formulario (`form-conductor`, `form-vehiculo`, etc.) tiene un **listener de `submit`**.
- Detecta si está en **modo edición** (`data-edit-id`):
  - Si existe `PUT /api/X/:id`.
  - Si no existe `POST /api/X`.
- Los botones cambian de estilo y texto según el modo:
  - Crear "Registrar"
  - Editar "Actualizar"
---
##  6. Flujo General
```plaintext
Login.html
   │
   ▼
Verificar token en localStorage
   │
   ├── No hay token → Redirige a Login
   └── Hay token → Acceso al sistema
        │
        ├── Cargar tablas (CRUD)
        ├── Formularios (Crear/Editar)
        ├── Mensajes globales
        └── Estadísticas (Chart.js)
