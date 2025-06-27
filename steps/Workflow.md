## 🚀 Comenzando

1. Haz clic en el botón **Use this template** para crear una copia de este repositorio.
2. Trabajarás directamente desde tu repositorio en GitHub.

---

## ⚙️ Configuración de GitHub Actions

1. En la raíz del proyecto, crea el archivo:  
   `.github/workflows/test_calculator.yml`
2. Copia y pega el contenido del workflow YAML (proporcionado más abajo).
3. Haz **commit** y **push** de los cambios.

---

## 🧪 ¿Qué hace este workflow?

- Se define el evento (`on: push`) y el sistema operativo (`runs-on`).

- Los pasos:
    - Realiza el **checkout** del código.
    - Instala **Node.js** y las dependencias del proyecto.
    - Ejecuta las **pruebas automatizadas** usando Node.
    - Genera un archivo `test-results.txt` con los resultados.
    - Carga ese archivo como **artefacto** en el pipeline de GitHub Actions para su descarga posterior.

---

## 📦 Ver artefactos en GitHub Actions

Una vez que se ejecute el workflow en GitHub Actions:

1. Ve a la pestaña **Actions** de tu repositorio.
2. Selecciona la ejecución más reciente (por ejemplo, *Run Tests and Upload Artifact*).
3. Desplázate hasta la sección **Artifacts** (al final del resumen).
4. Verás un enlace llamado **test-results**.
5. Haz clic para descargar un archivo `.zip` que contiene el archivo `test-results.txt`.
6. Abre el archivo para revisar los resultados de las pruebas, por ejemplo:

---

## 📝 Código

```yaml
name: Run Tests and Upload Artifact

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: 22

      - name: Install dependencies
        run: npm install

      - name: Run tests and generate report
        run: node test/calculator.test.js

      - name: Upload artifact
        uses: actions/upload-artifact@v4
        with:
          name: test-results
          path: results/test-results.txt
```
