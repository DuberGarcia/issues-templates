
# HU-004: Implementación Frontend – Formulario Plan Básico (Paso 2 – Productos Iniciales)

## Información General

**ID:** HU-004  
**Módulo:** vinculaciones  
**Tipo:** Desarrollo Frontend  
**Prioridad:** Media  
**Estimación:** 13 puntos  
**Sprint:** Por definir  

---

## Historia de Usuario

**Como** Desarrollador Frontend del equipo Atlantis Nexus  

**Quiero** implementar el **Paso 2 del Formulario de Plan Básico**, permitiendo la selección y configuración de productos iniciales  

**Para** que los usuarios puedan definir los productos financieros a vincular (Aportes, Fondo Mutual, Ahorro a la Vista), con validaciones claras, reglas de negocio aplicadas y una experiencia accesible y guiada

---

## Alcance de la Historia

### Incluye
- Implementación del formulario Paso 2
- Tabla dinámica de productos
- Selección / deselección de productos
- Validaciones por producto
- Campos adicionales de oficinas
- Navegación entre pasos
- Accesibilidad WCAG 2.1 AA
- Responsive design

### No incluye
- Persistencia en backend
- Cálculos financieros finales
- Confirmación transaccional
- Diseño UX/UI (ya aprobado)

---

## Descripción Técnica

### 1. Página (Smart Component)

**Archivo:** `plan-basico-paso2-page.component.ts`

Responsabilidades:
- Construir el Reactive Form del Paso 2
- Inicializar productos obligatorios y opcionales
- Gestionar habilitación / deshabilitación de filas
- Coordinar navegación entre pasos
- Controlar estado del botón Confirmar

---

### 2. Componentes Presentacionales (Dumb)

- `productos-table.component.ts`

Responsabilidades:
- Renderizado visual
- Inputs / Outputs
- Sin reglas de negocio

---

## Accesibilidad (Obligatorio)

- Tabla con `<table>`, `<thead>`, `<tbody>`, `<th>`
- Checkboxes con `<label>` asociado
- Campos requeridos con `aria-required="true"`
- Campos disabled con `aria-disabled="true"`
- Mensajes de error con `role="alert"`
- Navegación completa por teclado
- Cumple WCAG 2.1 nivel AA

---

## Especificación Técnica

### Tecnologías
- Angular 20 (Standalone Components)
- Reactive Forms (FormArray)
- Angular Signals (estado local)
- ChangeDetectionStrategy.OnPush
- Tailwind CSS 4.x

---

### Modelo de Datos

```ts
export interface ProductoPlanBasico {
  codigo: 'APORTES' | 'FONDO_MUTUAL' | 'AHORRO_VISTA';
  seleccionado: boolean;
  modalidadPago?: string;
  valor?: number;
  permanencia?: number;
  obligatorio: boolean;
}
```

---

### Reglas de Negocio – Frontend

#### Aportes (Obligatorio)
- Siempre seleccionado
- Campos disabled
- Modalidad fija: NÓMINA
- Valor fijo: 71000
- No se puede deseleccionar

#### Productos Opcionales
- Fondo Mutual
- Ahorro a la Vista

Comportamiento:
- Al seleccionar → habilitar campos
- Al deseleccionar → confirmar, limpiar y deshabilitar
- Validar modalidad y valor mínimo

---

### Validaciones

- Modalidad requerida si el producto está seleccionado
- Valores:
  - Fondo Mutual ≥ 15.600
  - Ahorro a la Vista ≥ 1.000
- Permanencia:
  - Opcional
  - Rango 1–99
- Oficinas:
  - Oficina que vincula (requerida)
  - Oficina que tramita (requerida)

---

## Estructura de Carpetas

```
modules/vinculaciones/
├── pages/
│   └── plan-basico/
│       ├── pages/
│       │   └── paso-2/
│       │       ├── plan-basico-paso2.page.ts
│       │       ├── plan-basico-paso2.page.html
│       │       └── plan-basico-paso2.page.spec.ts
│       │
│       ├── components/
│       │   └── productos-table/
│       │       ├── productos-table.component.ts
│       │       ├── productos-table.component.html
│       │       └── productos-table.component.spec.ts
```

---

## UI Principal (Segun UX/UI)

### Header del Formulario
- Badge "PLAN BASICO" en esquina superior derecha
- Color: #FFFFFF sobre #3B82F6
- Tipografia: Roboto Medium 12px
- Titulo de seccion: "Productos iniciales" (Roboto Bold, 24px, #111827)
- Card principal:
  - Background #FFFFFF
  - Border 2px solid #3B82F6
  - Radius 16px
  - Shadow 0 4px 12px rgba(0,0,0,0.1)
  - Padding 40px
  - Max-width 720px

---

### Tabla de Productos

Columnas:
1. Checkbox (sin header)
2. Producto
3. Modalidad de Pago
4. Valor Inicial/Mes
5. Permanencia (Anos)

Header:
- Background #E5E7EB
- Font weight 600, size 14px
- Color #374151
- Padding 12px 16px

Filas:
- Padding 12px 16px
- Border bottom 1px #E5E7EB
- Hover #F9FAFB

**Fila Aportes (obligatorio)**
- Checkbox checked y disabled
- Modalidad "NOMINA" deshabilitada
- Valor "$71.000" deshabilitado
- Permanencia deshabilitada

**Fila Fondo mutual**
- Checkbox habilitado
- Modalidad select habilitada
- Valor editable (minimo $15.600)
- Permanencia editable

**Fila Ahorro a la vista**
- Checkbox habilitado
- Modalidad select habilitada
- Valor editable (minimo $1.000)
- Permanencia editable

---

### Campos Adicionales (Oficinas)
- Grid 2 columnas, gap 24px
- "Oficina que vincula" y "Oficina que tramita" requeridos
- Height 44px, radius 8px
- Margin top 32px desde la tabla

---

### Stepper
- Paso 1 navegable (gris)
- Paso 2 activo (verde #10B981)
- Circulos 40px, gap 16px

---

### Botones de Accion
- Limpiar: outline, borde #D1D5DB, hover #F9FAFB
- Confirmar: primario verde #10B981
- Gap 16px, alineacion derecha

---

## Comportamiento

### Confirmar
- Habilitado solo si:
  - Productos seleccionados son válidos
  - Oficinas seleccionadas
  - Sin errores
- Acción:
  - Validar todo
  - Scroll al primer error si existe
  - Emitir datos y navegar a confirmación

### Limpiar
- Muestra modal de confirmación
- Limpia productos opcionales
- Mantiene Aportes
- Permanece en Paso 2

### Navegación
- Stepper permite volver al Paso 1 sin validar
- Datos se conservan en memoria

---

## Criterios de Aceptación – Frontend

### Funcionales
- [ ] Tabla renderiza productos correctamente
- [ ] Aportes no es editable ni deseleccionable
- [ ] Productos opcionales habilitan/deshabilitan campos
- [ ] Valores monetarios con formato correcto
- [ ] Oficinas son obligatorias
- [ ] Navegación entre pasos funcional

### Técnicos
- [ ] Standalone Components
- [ ] Reactive Forms con FormArray
- [ ] Validadores reutilizables
- [ ] OnPush habilitado
- [ ] Cumple lineamientos Atlantis Nexus

### Accesibilidad
- [ ] Tabla semántica
- [ ] Navegación por teclado
- [ ] Focus visible
- [ ] Contraste AA

---

## Pruebas

- Unit tests:
  - Lógica de selección de productos
  - Validadores de valor mínimo
  - Estados disabled
  - Navegación
- Archivos:
  - `plan-basico-paso2-page.component.spec.ts`
  - `productos.validators.spec.ts`

---

## Entregables

- Implementación Angular Paso 2
- Tests unitarios
- Documentación técnica

---

## Dependencias

### Previas
- Catálogo de productos
- Catálogo de modalidades
- Catálogo de oficinas

---

## Notas Técnicas

- No hardcodear valores (usar config)
- Formatear moneda con `Intl.NumberFormat`
- Tabla preparada para futuros productos
- Mantener separación Smart / Dumb

---

## Historial de Cambios

| Versión | Fecha | Autor | Cambios |
|-------|------|-------|--------|
| 1.1 | 2026-01-19 | Frontend | Adaptación desde HU UX/UI |
