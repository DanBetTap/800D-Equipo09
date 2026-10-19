# BalanCore

App móvil de **entrenamiento + nutrición** en un solo lugar.

**Equipo:** Isaías Vejar · Paz Osorio · Danilo Bettancourt
**Metodología:** Ágil (Scrum/Kanban)

## Estado actual

- MVP funcional, **offline-first**.
- **351 pruebas automatizadas** en **18 archivos**; `flutter analyze` sin incidencias.
- Flutter **3.47.3** (stable) · Dart **3.13.3**.

## Funcionalidades

- **Cuenta:** registro e inicio de sesión con correo o Google, verificación de correo, recuperación de contraseña y onboarding con cálculo de metas.
- **Perfil:** edición de datos, cambio de correo/contraseña/usuario, historial de peso e historial de entrenamiento por semanas/meses con figura muscular.
- **Nutrición:** registro manual (g/ml/ud), búsqueda en Supermercado/Extras/código de barras (Open Food Facts), «Mis alimentos», recetas con porciones (½–2x), totales del día vs objetivo y vista semanal.
- **Entrenamiento:** rutinas semanales, registro de series (reps/peso/tipo), supersets, descanso con notificaciones, récords personales (PR), historial, contador de pasos y logros.
- **Asistente de rutina:** motor de reglas siempre disponible y, opcionalmente, IA (Gemini) con caída automática a reglas.
- **Sin conexión:** cola local de series/comidas/rutinas y caché de lectura para consultar datos sin red.
- **Seguridad:** Firestore con reglas por usuario, Firebase App Check y clave de IA cifrada en el dispositivo.

## Tecnologías

Flutter (Dart), Riverpod, Firebase Auth, Cloud Firestore, Firebase App Check, Open Food Facts, `flutter_secure_storage`.
IA opcional con **Gemini**: clave propia del usuario **o** un **proxy gratuito** en Cloudflare Workers / Deno Deploy (`server/ai_proxy/`).

## Ejecutar

```bash
git clone https://github.com/Poxelado/BalancoreApp.git
cd BalancoreApp
flutter pub get
flutter run
```

## IA (opcional)

La app funciona sin IA (generador por reglas). Para activarla:

```bash
# Opción recomendada: con el proxy (la clave vive en el servidor).
flutter run --dart-define=AI_PROXY_URL=https://<tu-worker>.workers.dev

# Alternativa: clave de Gemini propia.
flutter run --dart-define=GEMINI_API_KEY=<clave>
```

Ver `server/ai_proxy/README.md` para desplegar el proxy (gratis, sin tarjeta).

## Estructura

```
lib/
  core/        tema, offline, IA, notificaciones, logros, pasos, alimentos
  features/
    auth/      registro, login, verificación, onboarding
    profile/   perfil, nutrición, recetas, historial, ajustes
    training/  rutinas, sesión de entreno, ejercicios, asistente IA
server/
  ai_proxy/    Cloudflare Worker que oculta la clave de IA (opcional)
```

## Documentación APT (Word)

1. Product Vision
2. Product Backlog y DoD
3. Documento de Diseño
4. Sprints (backlogs y retros)
5. Plan de Pruebas
6. Manual Técnico
7. Innovación
