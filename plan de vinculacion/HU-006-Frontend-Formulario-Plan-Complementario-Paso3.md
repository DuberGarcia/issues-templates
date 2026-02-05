# HU-006: Implementación Frontend – Formulario Plan Complementario (Paso 3 - Gestión de Beneficiarios)

## Información General

**ID:** HU-006  
**Módulo:** vinculaciones  
**Tipo:** Desarrollo Frontend  
**Prioridad:** Alta  
**Estimación:** 13 puntos  
**Sprint:** Por definir  

---

## Historia de Usuario

**Como** Desarrollador Frontend del equipo Atlantis Nexus  

**Quiero** implementar el **Formulario Plan Complementario – Paso 3** para la gestión de beneficiarios del grupo familiar  

**Para** permitir al responsable del plan agregar, editar y administrar beneficiarios con validaciones completas, estados de vinculación/gestión y una experiencia accesible y consistente con el diseño UX/UI aprobado

---

## Alcance de la Historia

### Incluye
- Implementación del Paso 3 (gestión de beneficiarios)
- Tabla dinámica con 7 columnas y estados por beneficiario
- CRUD mediante modales (agregar, editar, ver, eliminar)
- Menú contextual de acciones (⋮)
- Validaciones por parentesco, edad y duplicidad
- Stepper de 3 pasos (1 y 2 navegables, 3 activo)
- Accesibilidad WCAG 2.1 AA
- Responsive design

### No incluye
- Persistencia backend
- Cálculos financieros finales de descuentos
- Integración con servicios externos de validación
- Diseño UX/UI (ya aprobado)

---

## Descripción Técnica

### 1. Página (Smart Component)

**Archivo:** `plan-complementario-paso3-page.component.ts`

Responsabilidades:
- Inicializar el FormArray de beneficiarios
- Orquestar la apertura/cierre de modales
- Coordinar acciones CRUD y validaciones globales
- Gestionar estado del stepper y navegación
- Controlar habilitación de botones (Continuar / Limpiar)

---

### 2. Componentes Presentacionales (Dumb)

- `beneficiarios-table.component.ts`

Responsabilidades:
- Renderizado visual según UX/UI
- Inputs / Outputs
- Sin reglas de negocio

---

## Accesibilidad (Obligatorio)

- Botón "Agregar Familiar" con `aria-label`
- Menú contextual con roles correctos (`role="menu"`, `role="menuitem"`)
- Mensajes de error con `role="alert"`
- Estados `focus-visible` en botones y acciones
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
- UI Atlantis Nexus

---

### Modelo de Datos

```ts
export interface Beneficiario {
  id: string;
  tipoIdentificacion: string;
  numeroIdentificacion: string;
  primerApellido: string;
  segundoApellido?: string;
  primerNombre: string;
  segundoNombre?: string;
  fechaNacimiento: string;
  parentesco: 'CONYUGE' | 'HIJO_A' | 'OTRO';
  celular?: string;
  email?: string;
  direccion?: string;
  valorDctoCaja?: string;
  valorDctoNomina?: string;
  estadoVinculacion: 'EN_REGISTRO' | 'VINCULADO' | 'RECHAZADO';
  estadoGestion: 'REGISTRO_DATOS' | 'CONSULTA_LISTAS' | 'EVALUACION_CUPO' | 'GESTION_FINALIZADA';
}
```

---

## UI Principal (Segun UX/UI)

### Card
- Background: #FFFFFF
- Border: 2px solid #A855F7
- Border radius: 16px
- Padding: 40px
- Max-width: 1200px

### Badge Identificador
- Texto: PLAN COMPLEMENTARIO
- Color: #FFFFFF sobre #A855F7
- Posicion: esquina superior derecha
- Tipografia: Roboto Medium 12px

### Boton Agregar Familiar
- Centrado arriba de la tabla
- Background: #4ADE80
- Icono + a la izquierda
- Hover: #22C55E

---

## Tabla de Beneficiarios

Columnas:
1. Producto (Nombre completo)
2. Parentesco
3. Vr.Dcto.Caja
4. Vr.Dcto.Nomina
5. Estado Vinculacion
6. Estado Gestion
7. Acciones (sin header)

Comportamiento:
- Hover en filas: #F9FAFB
- Menu contextual por fila (⋮)
- Estados con badges segun HU-001

---

## Modal Agregar / Editar

Campos requeridos:
- Tipo de identificacion
- Numero de identificacion
- Primer apellido
- Primer nombre
- Fecha nacimiento
- Parentesco

Campos opcionales:
- Segundo apellido
- Segundo nombre
- Celular
- Email
- Direccion
- Vr.Dcto.Caja
- Vr.Dcto.Nomina

---

## Stepper

- Paso 1 y 2 navegables (sin validar)
- Paso 3 activo (verde)
- Gap 16px

---

## Comportamiento y Reglas de Negocio

- No permite continuar sin beneficiarios
- No permite identificaciones duplicadas
- Valida parentesco y edad minima/mxima por parentesco
- Limite maximo de beneficiarios configurable
- Resalta filas con errores
- Confirmacion para eliminar beneficiario
- Confirmacion para limpiar todos los beneficiarios
- Cambios se reflejan inmediatamente en la tabla

---

## Estructura de Carpetas

```
modules/vinculaciones/
├── pages/
│   └── plan-complementario/
│       ├── pages/
│       │   └── paso-3/
│       │       ├── plan-complementario-paso3.page.ts
│       │       ├── plan-complementario-paso3.page.html
│       │       └── plan-complementario-paso3.page.spec.ts
│       │
│       ├── components/
│       │   ├── beneficiarios-table/
│       │   │   ├── beneficiarios-table.component.ts
│       │   │   ├── beneficiarios-table.component.html
│       │   │   └── beneficiarios-table.component.spec.ts
│       │   ├── beneficiario-modal/
│       │   │   ├── beneficiario-modal.component.ts
│       │   │   ├── beneficiario-modal.component.html
│       │   │   └── beneficiario-modal.component.spec.ts
│       │   └── beneficiario-actions-menu/
│       │       ├── beneficiario-actions-menu.component.ts
│       │       ├── beneficiario-actions-menu.component.html
│       │       └── beneficiario-actions-menu.component.spec.ts
│       │
│       ├── services/
│       │   └── beneficiarios-state.service.ts
│       │
│       ├── models/
│       │   └── beneficiario.model.ts
│       │
│       └── plan-complementario.routes.ts
└── shared/
    └── utils/
        └── validators.ts
```

---

## Criterios de Aceptacion – Frontend

### Funcionales
- [ ] Badge "PLAN COMPLEMENTARIO" visible en morado
- [ ] Boton "Agregar Familiar" centrado y funcional
- [ ] Tabla renderiza 7 columnas con datos correctos
- [ ] CRUD completo de beneficiarios (agregar, editar, eliminar)
- [ ] Menu contextual (⋮) muestra Ver / Editar / Eliminar
- [ ] Stepper: pasos 1 y 2 navegables, paso 3 activo
- [ ] Boton Continuar deshabilitado si hay errores o sin beneficiarios
- [ ] Boton Limpiar elimina todos con confirmacion

### Diseno
- [ ] Header de tabla con fondo #E5E7EB
- [ ] Hover de filas con #F9FAFB
- [ ] Badges de estado con border-radius 16px
- [ ] Boton Continuar verde #10B981
- [ ] Borde del card morado #A855F7
- [ ] Separador horizontal gris 1px
- [ ] Stepper activo en verde

### Validaciones
- [ ] No permite continuar sin beneficiarios
- [ ] No permite identificaciones duplicadas
- [ ] Valida parentesco y edad por beneficiario
- [ ] Resalta filas con errores
- [ ] Confirma antes de eliminar o limpiar

---

## Pruebas

- Tests unitarios:
  - Validaciones de beneficiarios
  - CRUD en FormArray
  - Bloqueo de boton Continuar
  - Estados de tabla y menu contextual
- Archivos:
  - `plan-complementario-paso3.page.spec.ts`
  - `beneficiarios-table.component.spec.ts`
  - `beneficiario-modal.component.spec.ts`

---

## Entregables

- Implementacion Angular Paso 3
- Tests unitarios
- Documentacion tecnica

---

## Dependencias

- HU-001 (Estados de gestion/vinculacion)
- Libreria UI Atlantis Nexus
