# Instrucciones de Despliegue

## Opción 1: GitHub Pages (Recomendada)

### Paso 1: Crear repositorio en GitHub
1. Ve a https://github.com/new
2. Nombre: `propuesta-pice-pdf-excel`
3. Privado o Público (según prefieras)
4. No inicializar con README

### Paso 2: Subir código
```bash
cd /home/ubuntu/.openclaw/workspace/propuesta-pice-pdf-excel
git remote add origin https://github.com/TU_USUARIO/propuesta-pice-pdf-excel.git
git branch -M main
git push -u origin main
```

### Paso 3: Activar GitHub Pages
1. En el repo, ve a **Settings** → **Pages**
2. Source: **Deploy from a branch**
3. Branch: **main** / **root**
4. Guardar

### Paso 4: Personalizar
- Edita `index.html` con los datos específicos:
  - Nombre de la empresa cliente
  - Nombres del equipo
  - Nombre del manager y monitor
  - Datos específicos del proyecto (tiempos, volúmenes, etc.)

## Opción 2: Descargar y usar localmente

```bash
# Clonar o descargar el repo
cd propuesta-pice-pdf-excel

# Abrir en navegador
# Opción A: Simplemente abrir index.html
open index.html  # Mac
xdg-open index.html  # Linux

# Opción B: Servidor local Python
python3 -m http.server 8000
# Visitar http://localhost:8000
```

## Opción 3: Exportar a PDF

### Desde el navegador:
1. Abrir la página en Chrome/Edge
2. Ctrl+P (o Cmd+P en Mac)
3. Destino: "Guardar como PDF"
4. Márgenes: Mínimos
5. Opciones: Incluir gráficos de fondo ✅

### Usando herramientas CLI:
```bash
# Con Node.js y Puppeteer
npm install -g puppeteer
cd propuesta-pice-pdf-excel
node -e "
const puppeteer = require('puppeteer');
(async () => {
  const browser = await puppeteer.launch();
  const page = await browser.newPage();
  await page.goto('file://' + process.cwd() + '/index.html', {waitUntil: 'networkidle2'});
  await page.pdf({path: 'Propuesta_PICE.pdf', format: 'A4', printBackground: true});
  await browser.close();
})();
"
```

## Personalización Rápida

### Cambiar colores
Edita `assets/styles.css` y modifica las variables CSS al inicio:
```css
:root {
  --color-primary: #1a1a2e;    /* Azul oscuro actual */
  --color-highlight: #e94560;   /* Rojo/Rosa actual */
  /* Cambiar a tus colores corporativos */
}
```

### Cambiar fuentes
En `index.html`, reemplaza el Google Fonts:
```html
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap" rel="stylesheet">
```

Y actualiza en CSS:
```css
--font-heading: 'Roboto', sans-serif;
--font-body: 'Roboto', sans-serif;
```

## Estructura de archivos

```
propuesta-pice-pdf-excel/
├── index.html          # Documento principal
├── assets/
│   └── styles.css      # Estilos
├── docs/               # Documentación adicional (opcional)
└── anexos/             # Anexos del proyecto
```

## Notas importantes

- El documento es **responsive** (se ve bien en móvil y desktop)
- Usa **fuente Inter** para cuerpo y **Poppins** para títulos
- Incluye navegación sticky para fácil acceso
- Optimizado para impresión (oculta nav, ajusta colores)
- Carga rápida (sin dependencias externas pesadas)

## Soporte

Para dudas sobre el contenido PICE, consultar:
- Guía del curso PICE 2026-10
- Plantilla corporativa oficial
- Tutorías del Centro de Español (para revisión de redacción)
