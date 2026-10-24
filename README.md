# Organizador de imágenes con IA para GitHub

## Qué hace
- Se ejecuta al subir archivos nuevos a `Practicas/**` en la rama `main`.
- Analiza imágenes nuevas mediante la API de OpenAI con visión.
- Renombra solo las imágenes nuevas con nombres descriptivos en español.
- Crea o actualiza `Incluye.txt` en la carpeta donde estaba cada imagen.
- Hace commit y push de los cambios con `GITHUB_TOKEN`.

## Requisitos
- Repositorio GitHub con rama `main`.
- API key de OpenAI con acceso y saldo/límite disponible.
- GitHub Actions habilitado.
- Permiso de escritura de contenidos para el `GITHUB_TOKEN`.

## Instalación
1. Copia estos archivos a la raíz de tu repositorio.
2. En GitHub abre **Settings → Secrets and variables → Actions → New repository secret**.
3. Crea un secreto llamado `OPENAI_API_KEY` y pega tu clave de API. No la guardes en el código.
4. En **Settings → Actions → General → Workflow permissions**, permite lectura y escritura si tu configuración lo requiere.
5. Confirma que el workflow esté en `.github/workflows/organizar-imagenes.yml`.
6. Haz push de los archivos a la rama `main`.

## Uso
1. Crea una carpeta, por ejemplo `Practicas/23 de Octubre/`.
2. Sube una o varias imágenes a esa carpeta.
3. Haz commit y push a `main`.
4. Revisa la pestaña **Actions** y espera a que termine el workflow.
5. Verifica los nombres y `Incluye.txt` en GitHub.

## Prueba segura
Usa una carpeta de prueba como `Practicas/Prueba-IA/` con 1 o 2 imágenes no sensibles. Comprueba el resultado antes de subir material importante.

## Limitaciones y seguridad
- Solo procesa imágenes añadidas en el push; no vuelve a renombrar imágenes existentes.
- Formatos: PNG, JPG/JPEG, WEBP y GIF.
- Imágenes mayores de 10 MB se omiten con error visible.
- Los archivos se envían a la API de OpenAI para su análisis. No subas imágenes privadas o sensibles sin autorización.
- Las descripciones de IA pueden equivocarse: revísalas.
- Cada imagen analizada puede generar cargos según el modelo y uso de la API.
- El flujo se limita a la rama `main`. Si usas otra rama, cambia la condición del workflow.
- En el primer push del repositorio, solo analiza imágenes añadidas en el commit que disparó el flujo; no recorre todo el historial.
- El evento `workflow_dispatch` solo permite comprobar que el workflow se inicia; no procesa imágenes antiguas.
- GitHub no suele iniciar otro workflow cuando el commit se crea usando `GITHUB_TOKEN`; así se evita un bucle de ejecuciones.
