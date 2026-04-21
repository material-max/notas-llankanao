# 📘 Manual de Instalación y Uso
## Sistema de Notas + Portal de Apoderados
### Escuela Llankanao M.F.M.S. — Versión 2026

---

## 📦 Archivos incluidos

| Archivo | Descripción |
|---|---|
| `codigo-apps-script.gs` | Backend completo (sistema de notas + portal apoderados) |
| `index.html` | Sistema de notas para profesores y UTP |
| `portal-apoderado.html` | Portal de consulta para apoderados |
| `MANUAL.md` | Este documento |

---

## ⚙️ PASO 1 — Preparar el Apps Script

### 1.1 Abrir el editor

1. Ve a tu Google Sheet **"Base de Datos — Notas 2026"**
2. Menú: **Extensiones → Apps Script**
3. Se abre el editor de código

### 1.2 Reemplazar el código

1. Selecciona **todo el código existente** (Ctrl+A)
2. **Elimínalo** (Delete)
3. Abre el archivo `codigo-apps-script.gs` con el Bloc de notas
4. Selecciona todo (Ctrl+A) y copia (Ctrl+C)
5. Pégalo en el editor de Apps Script (Ctrl+V)
6. Guarda con **Ctrl+S**

> ⚠️ **Importante:** El nuevo código ya tiene tu `SHEET_ID` correcto. No lo cambies.

### 1.3 Verificar las hojas CONFIG y NOTAS

Si tu Sheet ya tiene las hojas **CONFIG** y **NOTAS**, salta al paso 1.4.

Si no las tiene (sistema completamente nuevo):

1. En el editor de Apps Script, busca la función `crearHojasAuxiliares` (al final del código)
2. Haz clic en el menú desplegable de funciones (arriba, donde dice "Seleccionar función")
3. Selecciona `crearHojasAuxiliares`
4. Haz clic en ▶ **Ejecutar**
5. Acepta los permisos si te los pide
6. Verifica en tu Sheet que se crearon las hojas CONFIG y NOTAS

> ⚠️ **No ejecutes** `crearHojasAuxiliares` si ya tienes notas guardadas. Solo crea hojas que no existen, no borra nada.

### 1.4 Publicar como aplicación web

1. Haz clic en **Implementar → Nueva implementación**
2. Haz clic en el ícono de engranaje ⚙️ y selecciona **Aplicación web**
3. Configura:
   - **Descripción:** Sistema Notas v2 Llankanao
   - **Ejecutar como:** Yo (tu cuenta)
   - **Quién tiene acceso:** Cualquier persona
4. Haz clic en **Implementar**
5. Acepta los permisos que te pida (es normal que los pida la primera vez)
6. **Copia la URL** que aparece — la necesitas en el paso 2

La URL tiene este formato:
```
https://script.google.com/macros/s/AKfycb.../exec
```
https://script.google.com/macros/s/AKfycbxEd-cgxWW9onn29Wt8HPoKqa74ExYF8NSn2N0US9Bm_Ozo5LLDwAwNItcSFZ2uoPYC/exec
---

## 🌐 PASO 2 — Configurar los archivos HTML

### 2.1 Configurar index.html

1. Abre `index.html` con el Bloc de notas (o VS Code)
2. Busca la línea (está cerca del inicio del `<script>`):
   ```javascript
   const API_URL = "PEGA_AQUI_LA_URL_DE_TU_APPS_SCRIPT";
   ```
3. Reemplaza el texto dentro de las comillas por la URL que copiaste en el paso 1.4:
   ```javascript
   const API_URL = "https://script.google.com/macros/s/AKfycb.../exec";
   ```
4. Guarda el archivo

### 2.2 Configurar portal-apoderado.html

Repite el mismo proceso:

1. Abre `portal-apoderado.html` con el Bloc de notas
2. Busca la misma línea `const API_URL = "PEGA_AQUI..."` 
3. Reemplaza con la misma URL
4. Guarda el archivo

---

## 🚀 PASO 3 — Subir a GitHub Pages

### 3.1 Crear el repositorio

1. Ve a [github.com](https://github.com) e inicia sesión
2. Haz clic en **New repository** (botón verde)
3. Configura:
   - **Repository name:** `sistema-notas-llankanao` (o el nombre que prefieras)
   - **Visibility:** Public ✅ (necesario para GitHub Pages gratuito)
   - Marca **Add a README file**
4. Haz clic en **Create repository**

### 3.2 Subir los archivos

1. En tu repositorio, haz clic en **Add file → Upload files**
2. Arrastra los 3 archivos:
   - `index.html`
   - `portal-apoderado.html`
   - `MANUAL.md` (opcional pero útil)
3. En "Commit changes", escribe: `Versión inicial del sistema`
4. Haz clic en **Commit changes**

### 3.3 Activar GitHub Pages

1. Ve a **Settings** (pestaña del repositorio)
2. En el menú izquierdo, haz clic en **Pages**
3. En "Source", selecciona **Deploy from a branch**
4. En "Branch", selecciona **main** y la carpeta **/ (root)**
5. Haz clic en **Save**
6. Espera 2-3 minutos

### 3.4 Obtener las URLs

Después de que GitHub Pages procese los archivos, las URLs serán:

- **Sistema de notas (profesores):**
  ```
  https://TU_USUARIO.github.io/sistema-notas-llankanao/
  ```
- **Portal de apoderados:**
  ```
  https://TU_USUARIO.github.io/sistema-notas-llankanao/portal-apoderado.html
  ```

Reemplaza `TU_USUARIO` con tu nombre de usuario de GitHub.

---

## ✅ PASO 4 — Verificar que funciona

### Verificar el sistema de notas

1. Abre la URL del sistema de notas
2. Debe aparecer el header **"Escuela Llankanao M.F.M.S"** y el punto verde **"Conectado"**
3. Ve a **⚙️ Administración** → selecciona un curso → debe cargar la lista de alumnos
4. Comprueba que la columna **RUT Apoderado** aparece (con "⚠ Sin cargar" en los que aún no tienen dato)

### Verificar el portal de apoderados

1. Abre la URL del portal
2. Haz clic en **Registrarme**
3. Ingresa:
   - Tu nombre
   - El RUT de un apoderado que ya cargaste en la hoja ALUMNOS (columna "Rut Apoderado")
   - Un correo y contraseña
4. Si el RUT está en la hoja ALUMNOS, el registro debe ser exitoso y mostrar los alumnos vinculados

---

## 📋 RESUMEN — Cómo funciona el sistema completo

### Sistema de notas (index.html) — Para profesores y UTP

| Módulo | Función |
|---|---|
| ✏️ Ingresar notas | Selecciona curso, asignatura y semestre. Ingresa hasta 8 notas por alumno. El promedio se calcula automáticamente. |
| 🔍 Consultar | Ve las notas de un alumno con vista semestral o anual. |
| 📄 Informes | Genera y descarga (PDF) informes por alumno o curso, semestrales o finales anuales. |
| ⚙️ Administración | Agrega, edita o elimina alumnos. Al agregar/editar, puedes cargar el RUT del apoderado para habilitar el portal. |

### Portal de apoderados (portal-apoderado.html) — Para familias

1. El apoderado se registra con **su propio RUT** (el mismo que UTP tiene en la matrícula)
2. El sistema busca en la hoja ALUMNOS todos los hijos que tienen ese RUT como apoderado
3. Se vinculan automáticamente (hermanos incluidos)
4. El apoderado puede ver notas por semestre o anual, y descargar el informe oficial en PDF
5. **Solo lectura** — no puede modificar nada

---

## 🗂️ Estructura de la hoja ALUMNOS

Tu hoja ALUMNOS debe tener exactamente estos encabezados en la fila 1:

| Columna | Nombre | Descripción |
|---|---|---|
| A | Curso | Ej: `1° Básico` |
| B | Nombre | Nombre completo en MAYÚSCULAS |
| C | NroLista | Número de lista (entero) |
| D | Rut | RUT del alumno |
| E | Rut Apoderado | RUT del apoderado (sin puntos, con guion es válido) |
| F | Nombre y Apellidos Apoderado | Nombre completo del apoderado |

> ⚠️ Los nombres de columna deben ser exactamente los indicados. El sistema los lee por nombre, no por posición.

---

## 🔄 Actualizar el sistema en el futuro

Cuando quieras hacer cambios al código:

**Para cambios en HTML (index.html o portal-apoderado.html):**
1. Edita el archivo localmente
2. En GitHub → tu repositorio → haz clic en el archivo → ícono de lápiz (editar) → pega el nuevo contenido → Commit

**Para cambios en Apps Script:**
1. Edita en el editor de Apps Script
2. Guarda (Ctrl+S)
3. **Implementar → Administrar implementaciones**
4. Haz clic en el **ícono de lápiz** de tu implementación
5. En "Versión" selecciona **Nueva versión**
6. Haz clic en **Implementar**

> ⚠️ Siempre usa "Editar → Nueva versión", NUNCA "Nueva implementación". Si creas una nueva implementación, la URL cambia y tendrías que actualizar ambos HTML.

---

## ❓ Solución de problemas frecuentes

| Problema | Causa | Solución |
|---|---|---|
| El punto de conexión aparece en **rojo** | La URL del Apps Script no está bien configurada en el HTML | Verifica que pegaste la URL correcta en `API_URL` |
| **"Acción no reconocida"** | El código del Apps Script es viejo | Verifica que pegaste el código nuevo completo y creaste una nueva versión de la implementación |
| **"No hay alumnos"** en Administración | El Sheet ID está incorrecto | El SHEET_ID en el código debe coincidir con el ID de tu Google Sheet |
| El apoderado recibe **"No encontramos ningún alumno"** | El RUT que ingresó no coincide con ningún "Rut Apoderado" en la hoja ALUMNOS | Verifica que el RUT esté cargado en la columna correcta |
| Las notas antiguas **no aparecen** | La URL del Apps Script cambió (nueva implementación) | Asegúrate de usar siempre la misma URL (editar implementación existente, no crear nueva) |
| **Error de permisos** al ejecutar el Apps Script | No aceptaste los permisos de Google | Vuelve al editor, ejecuta manualmente una función simple y acepta los permisos |

---

## 📞 Datos de configuración del sistema

Para referencia, estos son los datos cargados en la hoja CONFIG:

| Clave | Valor |
|---|---|
| nombreColegio | Escuela Llankanao M.F.M.S |
| director | Sr. Paulo Quezada V. |
| jefUTP | Sra. Gloria Barrera V. |
| rolBaseDatos | 3285-9 |
| region | Séptima del Maule |
| anioEscolar | 2026 |

Para modificar alguno de estos datos, puedes editar directamente las celdas de la hoja **CONFIG** en tu Google Sheet.

---

*Sistema desarrollado para uso interno de la Escuela Llankanao M.F.M.S. — Linares, Chile*
