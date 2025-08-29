# Sistema Avanzado de Gestión de Inventario — Almacenes Sony

Aplicación de consola en Python que implementa POO, colecciones y persistencia en SQLite
para gestionar el inventario de una tienda (caso: *Almacenes Sony*).

## Requisitos cubiertos

- **POO:** clases `Producto` (entidad) e `Inventario` (agregado/servicio de dominio).
- **Colecciones:** 
  - `dict[int, Producto]` para índice principal por `id` (búsqueda O(1)).
  - `set[str]` para nombres ya usados (validación rápida).
  - `list[Producto]` para listados y resultados de búsqueda.
  - `tuple` (mediante `ProductoSnapshot.to_tuple()`) para snapshots inmutables.
- **SQLite:** CRUD completo contra la tabla `productos`.
- **Interfaz:** menú interactivo en consola.

## Estructura de la base de datos

```sql
CREATE TABLE IF NOT EXISTS productos (
  id       INTEGER PRIMARY KEY,
  nombre   TEXT UNIQUE NOT NULL,
  cantidad INTEGER NOT NULL CHECK (cantidad >= 0),
  precio   REAL    NOT NULL CHECK (precio >= 0)
);
