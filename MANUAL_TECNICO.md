# 🛠️ Manual Técnico - Costos & Precios para Cocina

Documentación de arquitectura, fórmulas matemáticas y persistencia de la micro-aplicación de costeo gastronómico.

---

## 🏗️ 1. Arquitectura del Sistema

- **Arquitectura:** Single-Page Application (SPA) cliente puro, sin backend activo.
- **Frontend:** Vanilla HTML5, CSS3, JavaScript (ES6+).
- **Diseño & Estilos:** Tailwind CSS con paleta cálida gastronómica (`kitchenOrange`, `amber`, `slate-900`).
- **Persistencia:** Web Storage API (`localStorage`), con sincronización de exportación a JSON / CSV.
- **Librería QR:** `qrcode.min.js` empaquetada localmente con fallback automático a la API de QuickChart.io.

---

## 🧮 2. Fórmulas de Cálculo de Costos y Precios

### A. Costo Unitario de Insumo
$$\text{CostoUnitario} = \frac{\text{PrecioCompra}}{\text{CantidadPresentación}}$$
- Gramos: precio por gramo.
- Mililitros: precio por mililitro.
- Unidades: precio por unidad individual.

### B. Costo Total de Receta
$$\text{CostoTotal} = \sum (\text{CostoIngredientes}) + \sum (\text{CostoPackaging}) + \text{ManoDeObra} + \text{CostosIndirectos}$$
Donde:
- $\text{ManoDeObra} = \frac{\text{MinutosElaboración}}{60} \times \text{ValorHora}$
- $\text{CostosIndirectos} = (\sum \text{Ingredientes} + \sum \text{Packaging}) \times \%Gas$

### C. Costo Unitario por Modo de Venta
$$\text{CostoUnitarioFinal} = \frac{\text{CostoTotal}}{\text{Rendimiento}}$$

### D. Precio de Venta Sugerido (Markup sobre Costo)
$$\text{PrecioVenta} = \text{CostoUnitarioFinal} \times \left(1 + \frac{\%Ganancia}{100}\right)$$
$$\text{GananciaNeta} = \text{PrecioVenta} - \text{CostoUnitarioFinal}$$

---

## 🗄️ 3. Esquema de LocalStorage

### `cocina_profile_v1`
Datos de la marca del emprendimiento:
```json
{
  "name": "Costos · Mi Cocina",
  "subtitle": "mis recetas & precios 🍕🎂",
  "currency": "ARS",
  "hourlyRate": 3500,
  "gasPercent": 8,
  "logo": "data:image/jpeg;base64,..."
}
```

### `cocina_pantry_v1`
Listado de insumos y packaging:
```json
[
  {
    "id": "ins-101",
    "name": "Harina 000",
    "category": "ingrediente",
    "unit": "gr",
    "packageSize": 1000,
    "price": 1100,
    "costPerUnit": 1.10
  },
  {
    "id": "pack-201",
    "name": "Caja de Pizza 34cm",
    "category": "packaging",
    "unit": "un",
    "packageSize": 50,
    "price": 25000,
    "costPerUnit": 500
  }
]
```

### `cocina_recipes_v1`
Listado de recetas con composición y rendimientos:
```json
[
  {
    "id": "rec-301",
    "name": "Pizza Muzzarella Clásica",
    "mode": "unidad",
    "yield": 1,
    "laborMinutes": 20,
    "profitPercent": 85,
    "items": [
      { "pantryId": "ins-101", "quantity": 300, "enabled": true },
      { "pantryId": "pack-201", "quantity": 1, "enabled": true }
    ]
  }
]
```

---

## 🚀 4. Despliegue y Respaldos

- **Repositorio:** `https://github.com/JuanCDgo/costos-comida`
- **Branch:** `main`
- **Hosting:** GitHub Pages (`https://juancdgo.github.io/costos-comida/`)
- **Respaldo Google Drive:** Carpeta `costos-comida` (ID: `1TRPtXi67zkNoQXZ4yqebzO-0G_n85s24`).
