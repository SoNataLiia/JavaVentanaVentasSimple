# 🖥️ Ventana Ventas — Java Swing

Aplicación de escritorio desarrollada con **Java Swing** que muestra una ventana de búsqueda de clientes.

---

## 📁 Estructura del Proyecto

```
VentanaVentas/
└── src/
    ├── Main.java             ← Punto de entrada — solo lanza la aplicación
    └── VentanaVentas.java    ← Ventana principal con todos los componentes
```

> **¿Por qué dos clases?**
> Cada clase tiene una sola responsabilidad. `Main` solo sabe cómo arrancar el programa.
> `VentanaVentas` solo sabe cómo construir y mostrar la ventana. Esto hace el código
> más fácil de leer, mantener y ampliar.

---

## 🧩 Descripción de los Archivos

### `VentanaVentas.java`

Esta clase **extiende JFrame**, lo que significa que hereda todo el comportamiento
de una ventana estándar de Java (título, bordes, botón de cerrar, etc.) sin tener
que programarlo desde cero.

**Componentes de la ventana:**

| Componente | Tipo Java | Función |
|---|---|---|
| Título "Ventas" | `JLabel` | Texto grande y en negrita dentro de la ventana |
| Etiqueta "Cliente:" | `JLabel` | Texto descriptivo junto al campo |
| Campo de texto | `JTextField` | El usuario escribe el nombre del cliente |
| Botón | `JButton` | Lanza la búsqueda al hacer clic |

**Métodos del clase:**

`configurarVentana()` — Establece las propiedades básicas del JFrame: título de la
barra, tamaño en píxeles, comportamiento al cerrar, posición centrada en pantalla
y el sistema de distribución (layout).

`crearComponentes()` — Construye cada elemento visual y los añade al JFrame en
sus posiciones correctas usando `BorderLayout` (NORTH para el título, CENTER para
la fila de búsqueda).

`buscar()` — Método **privado** que contiene la lógica del botón. Es privado porque
ninguna otra clase necesita llamarlo directamente — es un detalle interno de esta
ventana. Valida que el campo no esté vacío y muestra un diálogo con el resultado.

---

### `Main.java`

El único trabajo de esta clase es **arrancar la aplicación correctamente**.

Usa `SwingUtilities.invokeLater()` para garantizar que la ventana se cree en el
hilo correcto de Swing (EDT — *Event Dispatch Thread*). Swing no es seguro para
múltiples hilos, así que toda la interfaz debe crearse en el EDT. Sin esta línea,
el programa podría funcionar la mayoría de las veces pero fallar de forma aleatoria.

---

## ▶️ Cómo Ejecutar

**Requisitos:** Java 17 o superior instalado.

**Desde IntelliJ IDEA:**
1. Abre el proyecto en IntelliJ.
2. Haz clic derecho sobre `Main.java`.
3. Selecciona **Run 'Main.main()'**.

**Desde la terminal:**
```bash
javac src/*.java -d out/
java -cp out Main
```

---

## 🏗️ Conceptos Clave Utilizados

**`extends JFrame`** — Herencia. La clase `VentanaVentas` hereda todo el
comportamiento de una ventana estándar de Java. Sin esto, tendríamos que
programar el título, los bordes y el botón de cerrar desde cero.

**`BorderLayout`** — Sistema de distribución que divide la ventana en 5 zonas:
NORTH (arriba), SOUTH (abajo), WEST (izquierda), EAST (derecha) y CENTER (centro).
El título va en NORTH, los controles en CENTER.

**`addActionListener(e -> buscar())`** — Escuchador de eventos. Le dice a Java:
*"cuando el usuario haga clic en este botón, ejecuta el método buscar()"*.
La flecha `->` es una expresión lambda — una forma corta de escribir una función anónima.

**`JOptionPane.showMessageDialog()`** — Muestra una ventana emergente estándar
con un mensaje. El primer parámetro `this` indica que el diálogo pertenece a
nuestra ventana (aparece centrado sobre ella).

**`SwingUtilities.invokeLater()`** — Garantiza que el código dentro se ejecute
en el hilo correcto para manejar la interfaz gráfica. Es una buena práctica
obligatoria en Swing.

---

## 📌 Trampas Comunes a Evitar

- **Olvidar `setVisible(true)`** → La ventana existe en memoria pero no aparece en pantalla.
- **Olvidar `setSize()` o `pack()`** → La ventana tendrá tamaño 0 y no se verá nada.
- **Escribir la lógica directamente en `addActionListener`** → Funciona, pero hace el código difícil de leer. Mejor llamar a un método separado como `buscar()`.
- **Crear la ventana fuera de `SwingUtilities.invokeLater()`** → Puede causar errores aleatorios difíciles de reproducir.

---

## 👩‍💻 Autora

Nataliia Sokhatska — CFGS DAM, Desarrollo de Interfaces 2025-2026
