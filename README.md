# GETO AI — Proyecto Android Studio (v2)

Aplicación Android nativa con Kotlin + Jetpack Compose, backend Node.js, memoria local, recordatorios y capacidades de voz e imágenes.

## Requisitos
- Android Studio reciente, JDK 17 y Android SDK 35.
- Node.js 18 o superior.
- Una clave de API de OpenAI. El uso de la API puede generar cargos según consumo y tarifas.

## Abrir la app
1. Descomprime el ZIP.
2. Abre Android Studio y selecciona **Open** sobre la carpeta `GETO_AI_Android`.
3. Espera a que Gradle sincronice y ejecuta en un emulador.

El emulador usa `http://10.0.2.2:3000/` para acceder al ordenador anfitrión.

## Configurar el servidor
En una terminal:
```bash
cd backend
cp .env.example .env
```
Edita `.env` y agrega tu clave:
```env
OPENAI_API_KEY=tu_clave_real
OPENAI_MODEL=gpt-4o-mini
PORT=3000
```
Luego:
```bash
npm install
npm start
```
Verifica `http://localhost:3000/health`.

**No incluyas la clave dentro de Android.** Para un teléfono físico en pruebas, cambia `API_BASE_URL` en `app/build.gradle.kts` por la IP local del ordenador y mantén ambos dispositivos en la misma red. Para producción usa HTTPS, autenticación y límites de uso.

## Funciones incluidas en esta versión
- Chat GETO en español con personalidad serena y elegante inspirada en ficción.
- Historial de conversación guardado localmente.
- Memoria editable y guardado automático básico para frases como "recuerda que...", "mi nombre es...", "prefiero..." y "estudio...".
- Dictado de mensajes con el reconocedor de voz disponible en Android.
- Lectura en voz alta de respuestas mediante Text-to-Speech del dispositivo.
- Adjuntar una imagen al chat para análisis visual mediante el modelo configurado en el backend.
- Recordatorios locales mediante notificaciones; se programan en minutos desde el momento actual.

## Limitaciones que aún requieren trabajo
- La memoria automática actual usa reglas sencillas; no es una memoria semántica que decida por sí sola qué es importante.
- El historial y memoria no se sincronizan entre dispositivos.
- La voz usa los servicios de reconocimiento y síntesis instalados en Android; su disponibilidad depende del dispositivo e idioma.
- El selector de imágenes envía la imagen como JPEG base64; algunos formatos pueden requerir conversión.
- Los recordatorios todavía no incluyen calendario por fecha/hora, recurrencia ni lista de tareas.
- El chat necesita Internet y el backend activo.
- Esta entrega contiene código fuente; no incluye un APK compilado ni Gradle Wrapper.
- Antes de publicar, configura HTTPS, autenticación, política de privacidad, cuotas y controles contra abuso.

## Seguridad
No publiques el backend sin autenticación y límites de uso. No compartas tu clave de API. Protege los datos personales guardados en el teléfono.


## Diseño B: elegante y futurista
La interfaz usa negro grafito, carbón azulado, detalles violetas y texto plateado.

## Generar APK automáticamente en GitHub
Este proyecto incluye `.github/workflows/build-apk.yml`. Sube el contenido del proyecto a un repositorio GitHub y ejecuta la acción **Build GETO AI APK** desde la pestaña Actions. Al terminar, descarga el artefacto `GETO-AI-debug-apk`. Es un APK de depuración para pruebas, no una versión firmada para publicar en Play Store.
