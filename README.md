# NN Records Desktop 🎵

Aplicación de escritorio oficial de [NN Records](https://nnrecords.app) para **Windows** y **macOS**, desarrollada con **Tauri v2** y **Rust**.

---

## ⚡ Características

- **Ultra ligera**: Instalador de solo ~1.7 MB (en contraste con los ~100 MB de aplicaciones basadas en Electron).
- **Bajo consumo de memoria**: ~30–50 MB de memoria RAM en ejecución.
- **Siempre actualizada**: Carga directamente la versión web oficial en alta fidelidad (`https://nnrecords.app`), recibiendo nuevas pistas, funciones y mejoras de diseño al instante sin necesidad de reinstalar.
- **Integración con el sistema**:
  - Controles multimedia integrados (teclas de volumen, Play/Pause en el teclado).
  - Ventana nativa optimizada con soporte para modo oscuro profundo.
  - Instalador nativo NSIS en español para Windows y `.dmg` para macOS (Apple Silicon e Intel).

---

## 🏗️ Arquitectura y Principios de Diseño

La aplicación está diseñada bajo el principio de **módulo profundo (Deep Module)**:
- **Interfaz mínima**: Un contenedor nativo ligero que encapsula el WebView del sistema operativo (WebView2 en Windows y WKWebView en macOS) bajo el identificador de User-Agent `NNRecords-Desktop/1.0`.
- **Implementación desacoplada**: Toda la lógica musical, base de datos y procesamiento vive en la plataforma web de NN Records. La aplicación nativa solo actúa como el adaptador de ventana ante el sistema operativo.

---

## 🚀 Compilación Local

### Requisitos previos
1. [Rust y Cargo](https://rustup.rs/) (versión stable).
2. [Node.js](https://nodejs.org/) (opcional, si se usa el CLI de tauri vía npm).
3. En Windows: Visual Studio C++ Build Tools y WebView2 (incluido por defecto en Windows 10 y 11).
4. En macOS: Xcode Command Line Tools.

### Instalación del CLI de Tauri v2
```bash
cargo install tauri-cli --version "^2.0.0" --locked
```

### Ejecutar en modo desarrollo
```bash
cargo tauri dev
```

### Compilar instalador para producción
```bash
# Compilación para el sistema operativo actual
cargo tauri build

# Compilación para macOS Apple Silicon (desde Mac)
cargo tauri build --target aarch64-apple-darwin

# Compilación para macOS Intel (desde Mac)
cargo tauri build --target x86_64-apple-darwin
```

Los ejecutables resultantes se ubicarán en `src-tauri/target/release/bundle/`.

---

## 📦 Pipeline de Despliegue Automatizado (GitHub Actions)

El repositorio incluye un flujo de integración continua en `.github/workflows/release.yml`.

### Cómo publicar una nueva versión:
Para generar los instaladores de Windows (`.exe`) y macOS (`.dmg`) y publicarlos automáticamente en **GitHub Releases**:

1. Incrementa la versión en `src-tauri/tauri.conf.json` y `src-tauri/Cargo.toml` (ej. `1.0.1`).
2. Crea y sube un tag de git:
   ```bash
   git tag v1.0.1
   git push origin v1.0.1
   ```
3. GitHub Actions compilará automáticamente en paralelo:
   - `NN-Records-Windows-setup.exe` (Windows x64 NSIS)
   - `NN-Records-Mac-AppleSilicon.dmg` (macOS Apple Silicon M1/M2/M3/M4)
   - `NN-Records-Mac-Intel.dmg` (macOS Intel)
4. Todos los instaladores quedarán adjuntos al Release correspondiente listos para descargar.

---

## 🛡️ Guía de Instalación para Usuarios (Avisos de Seguridad)

Al tratarse de una versión comunitaria de código abierto sin certificados comerciales de pago (EV/Apple Developer ID de $99–$400/año), los sistemas operativos muestran avisos de advertencia en las primeras descargas:

### En Windows (SmartScreen)
1. Al ejecutar el instalador `.exe`, aparecerá la pantalla azul: *"Windows protegió su PC / Editor desconocido"*.
2. Haz clic en el enlace **"Más información"** (*More info*).
3. Pulsa el botón **"Ejecutar de todas formas"** (*Run anyway*).

### En macOS (Gatekeeper)
1. Abre el archivo `.dmg` y arrastra **NN Records** a la carpeta **Aplicaciones**.
2. Al abrirla por primera vez, macOS indicará: *"Apple no puede comprobar si la app contiene malware"*.
3. Haz **clic derecho** (o `Control + Clic`) sobre la aplicación en Aplicaciones y selecciona **Abrir**.
4. Haz clic en **Abrir de todos modos**.
5. *(Alternativa por Terminal)*:
   ```bash
   xattr -cr /Applications/NN\ Records.app
   ```

---

## 📄 Licencia y Créditos

Desarrollado para [NN Records](https://nnrecords.app). Música y audio libres de copyright.
