# Godot Context Packer

[![Godot 4.x](https://img.shields.io/badge/Godot-4.x-4d88c4?style=flat-square&logo=godotengine&logoColor=white)](https://godotengine.org/)
[![100% Local](https://img.shields.io/badge/Privacidad-100%25_Local-2ea043?style=flat-square)](#privacidad-y-seguridad)
[![Zero Dependencies](https://img.shields.io/badge/Dependencias-Ninguna-555555?style=flat-square)](#)
[![Abrir App](https://img.shields.io/badge/Demo_en_Vivo-Abrir_Herramienta-4d88c4?style=flat-square)](https://jarenrafael.github.io/godot-context-packer/)

Empaquetador web ligero y **100% local** que convierte cualquier proyecto de **Godot 4.x** en un único archivo estructurado (`XML` o `TXT`), optimizado para darle contexto completo y preciso a modelos de inteligencia artificial sin saturar su límite de tokens.

### 👉 [Abrir Godot Context Packer en el navegador](https://jarenrafael.github.io/godot-context-packer/)

---

## ¿Por qué usar esta herramienta?

| Característica | Godot Context Packer | Plugins de AssetLib | Herramientas CLI (ej. Repomix) |
| :--- | :---: | :---: | :---: |
| **Instalación** | Ninguna (funciona en web) | En cada proyecto (`addons/`) | Requiere Node.js / terminal |
| **Ensucia el repositorio** | No | Sí (archivos extra en el juego) | No |
| **Limpieza de `.tscn` y `project.godot`** | Nativa para Godot 4.x | Variable | No (trata escenas como texto plano) |
| **Re-escaneo en 1 clic** | Sí | Sí | Manual por comando |

---

## Características principales

### 🧠 Análisis inteligente para Godot 4.x
* **Extractor quirúrgico de escenas (`.tscn`):** En *Modo Inteligente*, extrae únicamente el encabezado, recursos externos (`[ext_resource]`), jerarquía de nodos (`[node]`), scripts adjuntos y señales conectadas (`[connection]`), descartando bloques `SubResource` y coordenadas visuales repetitivas (ahorra hasta un **80% de tokens**). Incluye opción de *Modo Completo* si necesitas depurar shaders o recursos específicos.
* **Compresor de `project.godot`:** Extrae automáticamente el nombre del proyecto, la escena principal (`run/main_scene`), resolución, **Autoloads (Singletons)** y acciones del **InputMap**.
* **Rutas nativas `res://`:** Normaliza todas las rutas de archivos al formato interno de Godot (`res://scripts/player.gd`) para evitar errores de ruta en el código generado por la IA.
* **Higiene automática:** Detecta y omite archivos binarios (`.tres`/`.res` compilados) y oculta archivos `.uid` y `.import` generados por Godot 4.4+.

### ⚡ Flujo de trabajo rápido
* **Re-escaneo en 1 clic:** Tras guardar cambios en Godot, actualiza todo el paquete sin volver a navegar por tus carpetas.
* **Perfiles rápidos (Presets):** Cambia al instante entre *Solo Lógica* (`.gd`, `.cs`, `.json`), *Arquitectura Completa* (`.gd`, `.json`, `.tscn`, `project.godot`) o *Guiones y Datos* (`.json`, `.cfg`, `.md`, `.csv`).
* **Roles de IA integrados:** Incluye opcionalmente un *System Prompt* configurable al inicio del archivo (*Arquitecto Godot 4*, *Cazador de Bugs* o *Escritor de Guiones*).
* **Memoria local:** Guarda tus filtros, formato preferido y rol en `localStorage`.

### 🔒 Privacidad y control granular
* **Procesamiento 100% en tu navegador:** Tus archivos nunca se suben a ningún servidor; todo ocurre en la memoria RAM local.
* **Control por archivo y medidor de tokens:** Activa o desactiva archivos individuales viendo su peso estimado en tokens antes de exportar.
* **Soporte `.gitignore` y sanitizador:** Respeta las exclusiones de tu `.gitignore` y permite enmascarar patrones de claves API (`AIza...`, `sk-...`, tokens) antes de descargar o copiar.

---

## Ejemplo de salida optimizada (`XML`)

Así es como la herramienta transforma tu proyecto para que cualquier IA entienda exactamente cómo se conectan tus nodos y scripts:

```xml
<project_context engine="Godot 4.x">
  <project_tree>
    res://project.godot
    res://scenes/main.tscn
    res://scripts/player.gd
  </project_tree>

  <file path="res://scenes/main.tscn" mode="smart">
    [gd_scene load_steps=2 format=3]
    [ext_resource type="Script" path="res://scripts/player.gd" id="1_abc"]
    [node name="Main" type="Node2D"]
    [node name="Player" type="CharacterBody2D" parent="."]
    script = ExtResource("1_abc")
    [connection signal="body_entered" from="Area2D" to="Player" method="_on_area_entered"]
  </file>
</project_context>
```

---

## Cómo usarlo

1. Abre **[Godot Context Packer](https://jarenrafael.github.io/godot-context-packer/)**.
2. Haz clic en **Seleccionar carpeta del proyecto** y elige la carpeta raíz de tu juego (donde está `project.godot`).
3. Ajusta el preset, desmarca archivos si lo necesitas y revisa el medidor de tokens.
4. Haz clic en **Descargar** o **Copiar todo** y pégalo directamente en tu chat con la IA.

## Compatibilidad de navegadores

* **Chrome, Edge, Brave y Opera:** Soporte completo (incluye botón de **Re-escanear carpeta** en 1 clic mediante la *File System Access API*).
* **Firefox y Safari:** Totalmente funcionales mediante selector de carpeta estándar.
