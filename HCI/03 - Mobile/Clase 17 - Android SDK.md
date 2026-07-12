# Clase 17 - Android SDK

## Android Studio

- **IDE oficial** de Android, creado para acelerar el desarrollo de apps de calidad para todos los dispositivos Android.
- Basado en **IntelliJ IDEA**.
- Disponible para **Windows, macOS y Linux**.

### Paquete de Android Studio incluye
- Android Studio (IDE)
- Herramientas de línea de comandos del SDK
- Herramientas de compilación del SDK
- Complemento de Gradle para Android
- Emulador de Android

**No es suficiente** para desarrollar: debe complementarse con componentes dependientes de la plataforma (versión de Android): **Herramientas de la plataforma SDK** y **Plataforma de SDK**.

### Requerimientos (referencia)
- 8 GB RAM o superior (16 GB recomendado); 8 GB libres en disco (16 GB SSD recomendado); resolución 1280×800 mínimo.

## Estructura del Proyecto

- Cada proyecto incluye uno o más **módulos** con código fuente y recursos.
- Vista por defecto: **"Android"** (organizada por módulo). Para ver la estructura real en disco hay que cambiar a vista **"Proyecto"**.
- Los archivos de compilación están en **"Gradle Scripts"**.
- Cada módulo contiene:
  - **manifest**: archivo `AndroidManifest.xml`.
  - **kotlin+java**: archivos fuente Kotlin/Java (incluyendo pruebas unitarias JUnit).
  - **res**: recursos que no son código (layouts XML, strings de la UI, imágenes, etc.).

## Interfaz de Usuario (elementos)
1. Barra de herramientas (ejecutar app, iniciar herramientas del SDK).
2. Barra de navegación (navegar el proyecto, abrir archivos).
3. Ventana de edición (crear/modificar código; cambia según el tipo de archivo).
4. Barra de la ventana de herramientas (expandir/contraer ventanas).
5. Ventanas de herramientas (proyecto, búsqueda, control de versión).
6. Barra de estado (estado del proyecto/IDE, advertencias).

### Autocompletado de código
- **Básica**: sugerencias básicas (Ctrl+Space). Llamarla dos veces da más resultados.
- **Inteligente**: opciones según el contexto, reconoce tipo y flujo de datos (Ctrl+Shift+Space).
- **Sentencia**: completa la sentencia agregando paréntesis, llaves, etc. (Ctrl+Shift+Enter).

Reformatear código: **Ctrl+Alt+L**.

## Sistema de compilación Gradle

- Android Studio usa **Gradle** como base + el complemento de Android para Gradle (funciones específicas).
- Permite: personalizar/extender el proceso, crear **varios APK** con distintas funciones desde el mismo proyecto, reutilizar código y recursos.
- Archivos de compilación: `build.gradle.kts` (**Kotlin**) o `build.gradle` (**Groovy**).
- Cada proyecto tiene un archivo de compilación **de nivel superior** (para todo el proyecto) y archivos **de nivel de módulo** independientes.

### Administración de dependencias
- Se especifican por nombre en los archivos de compilación **a nivel de módulo**.
- Gradle busca las dependencias y las hace disponibles en tiempo de compilación.
- Tipos: dependencias de módulos, binarias remotas y binarias locales.
- Por defecto se usa el **repositorio central de Maven**.

## Herramientas del SDK

### Android SDK Manager
Herramienta que permite consultar, instalar, actualizar y desinstalar paquetes del SDK. Accesible desde Android Studio (**Tools > SDK Manager**) o vía `sdkmanager` (línea de comandos).

Paquetes:
- **Herramientas de línea de comandos del SDK** (requerido): avdmanager, lint, sdkmanager.
- **Herramientas de compilación del SDK** (requerido): generación del APK.
- **Herramientas de la plataforma del SDK** (requerido): incluye **adb** (Android Debug Bridge).
- **Emulador Android** (recomendado): basado en **QEMU**.
- **Plataforma del SDK de Android** (requerido): al menos una versión; recomendable la más reciente.
- **Imágenes del sistema Intel o ARM** (recomendado): obligatorias para el emulador. Para APIs de Google usar imágenes Google API o Google Play.
- Opcionales: Servicios de Google Play, Driver USB de Google (Windows), HAXM (**deprecado**), **AEHD** (Android Emulator hypervisor driver, reemplaza a Intel HAXM).

### Android Virtual Device (AVD) Manager
Un **AVD** es una configuración que define las características de un dispositivo (teléfono, tableta, Wear OS, Android TV, Automotive OS) a simular en el emulador. Accesible desde **Tools > AVD Manager** o vía `avdmanager`.

### Android Debug Bridge (adb)
Herramienta de línea de comandos para comunicarse con un dispositivo virtual (emulador) o físico (USB o Wi-Fi en Android 10+). Permite instalar/depurar apps y acceder a un shell de Unix. Programa **cliente-servidor** con tres componentes:
- **Cliente**: envía comandos (en la máquina de desarrollo, comando `adb`).
- **Demonio (adbd)**: ejecuta comandos en el dispositivo (segundo plano).
- **Servidor**: administra la comunicación cliente-demonio (en la máquina de desarrollo).

Habilitar depuración: activar **Depuración por USB** en **Opciones para desarrolladores** (a partir de Android 4.2 están ocultas: tocar 7 veces **Número de compilación** en "Acerca del dispositivo"). Android 4.2.2+ pide aceptar una **clave RSA** (mecanismo de seguridad).

### Android Emulator
Simula dispositivos Android en la computadora para probar apps sin dispositivos físicos. Casi todas las funciones de un dispositivo real (llamadas, SMS, ubicación, sensores, Play Store). Cada instancia usa un **AVD**.

- **Ventajas**: más económico, hardware reconfigurable, las pruebas no afectan al SO/datos del dispositivo.
- **Desventajas**: bastante lento, faltan características (bluetooth, USB), no garantiza que funcione igual que en un dispositivo físico.

## Preguntas típicas V/F

- Android Studio está basado en Eclipse → **Falso** (basado en IntelliJ IDEA).
- El emulador de Android está basado en QEMU → **Verdadero**.
- adb es un programa cliente-servidor con tres componentes (cliente, demonio, servidor) → **Verdadero**.
- El AndroidManifest.xml se ubica en la carpeta `res` → **Falso** (está en la carpeta `manifest`; `res` es para recursos no-código).
- Android Studio usa Maven como sistema de compilación base → **Falso** (usa **Gradle**; Maven es el repositorio de dependencias por defecto).
- Los archivos `build.gradle.kts` usan sintaxis Kotlin → **Verdadero**.
- El emulador es más rápido que un dispositivo físico → **Falso** (es bastante lento).
