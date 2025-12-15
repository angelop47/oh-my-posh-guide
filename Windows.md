# Guía de Configuración: Oh My Posh (Tema Clean-Detailed)

Esta guía te ayudará a configurar **Oh My Posh** en PowerShell con el tema **clean-detailed**.

---

## 0. Requisitos Previos

*   **PowerShell 7.2** o superior recomendado.
*   **Permisos de Administrador** para instalar fuentes y módulos.

---

## 1. Instalación de Oh My Posh

Abre tu terminal y ejecuta el siguiente comando para instalar Oh My Posh usando Winget:

```powershell
winget install JanDeDobbeleer.OhMyPosh --source winget
```

**Verificación:** Reinicia la terminal y comprueba que se instaló correctamente escribiendo:
```powershell
oh-my-posh --version
```

---

## 2. Configuración de Fuentes (Nerd Fonts)

Para que los iconos se vean bien, necesitas una fuente compatible. Recomendamos **Hack Nerd Font**.

1.  **Descargar**: [Hack Nerd Font (v3.4.0) - Enlace Directo](https://github.com/ryanoasis/nerd-fonts/releases/download/v3.4.0/Hack.zip) o visita [Nerd Fonts Downloads](https://www.nerdfonts.com/font-downloads).
2.  **Instalar**: Descomprime el archivo y haz doble clic en los archivos `.ttf` para instalarlos en Windows.

### Configurar Windows Terminal
Para usar la fuente, debes editar la configuración de **Settings (JSON)** en Windows Terminal.

Busca la sección `"defaults"` dentro de `"profiles"` y agrega (o modifica) la propiedad `font`:

```json
"profiles": {
    "defaults": {
        "font": {
            "face": "Hack Nerd Font Mono"
        },
        "opacity": 85
    }
}
```

---

## 3. Configuración del Tema y Perfil

### Descargar el Tema (Clean Detailed)
Creamos una carpeta para temas y descargamos el archivo de configuración:

```powershell
# Crear directorio si no existe
mkdir "$HOME\.oh-my-posh-themes" -Force

# Descargar el tema
Invoke-WebRequest `
  -Uri https://raw.githubusercontent.com/JanDeDobbeleer/oh-my-posh/main/themes/clean-detailed.omp.json `
  -OutFile "$HOME\.oh-my-posh-themes\clean-detailed.omp.json"
```

### Instalar Iconos de Terminal (Opcional pero recomendado)
Mejora la visualización de archivos y carpetas:

```powershell
Install-Module -Name Terminal-Icons -Repository PSGallery -Force
```

---

## 4. Configurar el Perfil de PowerShell

Haremos que Oh My Posh y los iconos carguen automáticamente al abrir PowerShell.

1.  Abre tu perfil de PowerShell con el bloc de notas:
    ```powershell
    # Crea el perfil si no existe
    if (!(Test-Path -Path $PROFILE)) { New-Item -ItemType File -Path $PROFILE -Force }
    
    # Abrir con Notepad
    notepad $PROFILE
    ```

2.  **Copia y pega** el siguiente bloque de código dentro del archivo que se abrió:

    ```powershell
    # --- Configuración de Oh My Posh y Terminal ---

    # 1. Iniciar Oh My Posh con el tema 'clean-detailed'
    oh-my-posh init pwsh --config "$HOME\.oh-my-posh-themes\clean-detailed.omp.json" | Invoke-Expression

    # 2. Cargar iconos para archivos y carpetas (si instalaste el módulo)
    Import-Module Terminal-Icons
    ```

3.  **Guarda** el archivo y cierra el bloc de notas.

---

## 5. Finalizar

Para ver los cambios, recarga tu perfil ejecutando:

```powershell
. $PROFILE
```

¡Listo! Tu terminal debería verse increíble ahora.
