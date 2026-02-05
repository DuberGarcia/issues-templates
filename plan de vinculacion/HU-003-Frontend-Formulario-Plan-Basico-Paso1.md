
# HU-003: Implementación Frontend – Formulario Plan Básico (Paso 1)

## Información General

**ID:** HU-003  
**Módulo:** vinculaciones  
**Tipo:** Desarrollo Frontend  
**Prioridad:** Media  
**Estimación:** 13 puntos  
**Sprint:** Por definir  

---

## Historia de Usuario

**Como** Desarrollador Frontend del equipo Atlantis Nexus  

**Quiero** implementar el **Formulario Plan Básico – Paso 1** como un formulario multipaso accesible y validado  

**Para** permitir que los usuarios registren una nueva vinculación básica de forma guiada, segura y sin errores, cumpliendo las reglas funcionales y técnicas definidas

---

## Alcance de la Historia

### Incluye
- Implementación del formulario Paso 1
- Reactive Forms con validaciones en tiempo real
- Búsqueda y autocompletado de asociado
- Navegación al Paso 2
- Accesibilidad WCAG 2.1 AA
- Responsive design

### No incluye
- Implementación del Paso 2
- Persistencia backend
- Reglas de negocio de dominio
- Diseño UX/UI (ya aprobado)

---

## Descripción Técnica

### 1. Página (Smart Component)

**Archivo:** `plan-basico-paso1-page.component.ts`

Responsabilidades:
- Inicializar el Reactive Form
- Gestionar estado del paso actual
- Manejar validaciones y errores
- Coordinar navegación entre pasos
- Integrar búsqueda de asociado

---

### 2. Componentes Presentacionales (Dumb)

- `plan-basico-form.component.ts`

Responsabilidades:
- Renderizado visual
- Inputs / Outputs
- Sin lógica de negocio

---

## Accesibilidad (Obligatorio)

- Todos los campos con `<label>` asociado
- Campos requeridos con `aria-required="true"`
- Mensajes de error con `role="alert"`
- Orden lógico de tabulación
- Estados `focus-visible`
- Cumple WCAG 2.1 nivel AA

---

## Especificación Técnica

### Tecnologías
- Angular 20 (Standalone Components)
- Reactive Forms
- Angular Signals (estado local)
- ChangeDetectionStrategy.OnPush
- Tailwind CSS 4.x

---

### Estructura de Formulario (Paso 1)

**Campos requeridos:**
- Tipo identificación
- Primer apellido
- Primer nombre
- Fecha nacimiento
- Email
- Modalidad de pago
- Ocupación
- Parentesco con el asociado que presenta (si hay asociado)

**Campos opcionales:**
- Segundo apellido
- Segundo nombre
- Celular
- Asociado que presenta
 - Nombre asociado que presenta (solo lectura)

---

### Validadores Personalizados

```ts
soloNumeros
soloLetras
emailValido
celularColombia
mayorEdad
identificacionPorTipo
```
---

## UI Principal (Segun UX/UI)

### Header del Formulario
- Badge "PLAN BASICO" en esquina superior derecha
- Color: #FFFFFF sobre #3B82F6
- Tipografia: Roboto Medium 12px
- Card principal:
  - Background #FFFFFF
  - Border 2px solid #3B82F6
  - Radius 16px
  - Shadow 0 4px 12px rgba(0,0,0,0.1)
  - Padding 40px
  - Max-width 720px

---

### Grid de Campos (2 Columnas)
- Distribucion 50% / 50%, gap 24px
- Inputs de 44px de alto, radius 8px

**Fila 1**
- Tipo de Identificacion (select)
- No. Identificacion (input con lupa verde)

**Fila 2**
- Primer apellido
- Segundo apellido (opcional)

**Fila 3**
- Primer nombre
- Segundo nombre (opcional)

**Fila 4**
- Fecha de nacimiento (date picker con icono)
- Celular (opcional)

**Fila 5**
- Email (ancho completo)

**Fila 6**
- Modalidad de pago (select)
- Ocupacion (select)

**Separador**
- Linea horizontal 1px #E5E7EB, margin vertical 32px

---

### Seccion Asociado que Presenta

**Fila 7**
- Asociado que presenta (70%, input con lupa)
- Parentesco con el asociado (30%, select, requerido si hay asociado)

**Fila 8**
- Nombre asociado que presenta (100%, solo lectura)
- Background #F9FAFB, texto #4B5563, cursor not-allowed

---

### Stepper
- Paso 1 activo (verde #10B981)
- Paso 2 inactivo (gris #E5E7EB)
- Circulos 40px, gap 16px

---

### Botones de Accion
- Limpiar: outline, borde #D1D5DB, hover #F9FAFB
- Continuar: primario gris #374151, icono flecha derecha
- Gap entre botones: 16px, alineacion derecha

---

## Reglas de Negocio y Validaciones

- Tipo de identificacion requerido (opcion valida)
- No. identificacion: solo numeros y longitud por tipo
- Nombres y apellidos: solo letras, minimo 2 caracteres
- Fecha de nacimiento: formato valido, no futura, mayor de edad
- Celular: formato colombiano (10 digitos, inicia con 3)
- Email: formato valido
- Modalidad de pago y ocupacion: opcion requerida
- Asociado que presenta: busqueda por identificacion
- Parentesco: requerido solo si hay asociado
- Nombre asociado: autocompletado y solo lectura

---

### Comportamiento

- Validación onBlur / onChange
- Botón Continuar habilitado solo si el formulario es válido
- Botón Limpiar con confirmación modal
- Navegación a `/vinculaciones/plan-basico/paso-2`

---

## Estructura de Carpetas

```
modules/vinculaciones/
├── pages/
│   └── plan-basico/
│       ├── pages/
│       │   └── paso-1/
│       │       ├── plan-basico-paso1.page.ts
│       │       ├── plan-basico-paso1.page.html
│       │       └── plan-basico-paso1.page.spec.ts
│       │
│       ├── services/
│       │   └── plan-basico.state.ts
│       │
│       └── plan-basico.routes.ts
└── shared
    └── utils/
        ├── validators.ts
        └── formatters.ts
```

---

## Criterios de Aceptación – Frontend

### Funcionales
- [ ] Badge "PLAN BASICO" visible en esquina superior derecha
- [ ] Card con borde azul #3B82F6 y padding 40px
- [ ] Grid de 2 columnas con los campos definidos
- [ ] Email y Nombre asociado ocupan ancho completo
- [ ] Seccion de asociado separada por linea horizontal
- [ ] Stepper muestra paso 1 activo y paso 2 inactivo
- [ ] Boton Limpiar abre confirmacion
- [ ] Boton Continuar navega a Paso 2 si el formulario es valido
- [ ] Autocompleta nombre del asociado si existe

### Técnicos
- [ ] Standalone Components
- [ ] Reactive Forms
- [ ] Validators reutilizables
- [ ] OnPush habilitado
- [ ] Cumple lineamientos Atlantis Nexus

### Diseño
- [ ] Tipografia Roboto aplicada en labels, inputs y botones
- [ ] Inputs con altura 44px y radius 8px
- [ ] Iconos de lupa y calendario visibles y alineados
- [ ] Hover de inputs aplica borde azul y ring
- [ ] Boton Continuar con color #374151

### Validaciones
- [ ] Requeridos bloquean continuar si estan vacios
- [ ] Identificacion valida longitud por tipo
- [ ] Nombres y apellidos solo letras
- [ ] Fecha de nacimiento valida mayoria de edad
- [ ] Celular valida formato colombiano
- [ ] Email valida formato correcto
- [ ] Parentesco requerido si hay asociado

### Accesibilidad
- [ ] Labels visibles
- [ ] Errores accesibles
- [ ] Navegación por teclado
- [ ] Contraste AA
 - [ ] aria-required en campos obligatorios
 - [ ] role="alert" en errores

### Responsividad
- [ ] < 768px el grid pasa a una columna
- [ ] Botones se apilan en mobile
- [ ] Padding del card se reduce en mobile

---

## Pruebas

- Tests unitarios:
  - Validadores personalizados
  - Estados del formulario
  - Navegación
- Archivos:
  - `plan-basico-paso1-page.component.spec.ts`
  - `plan-basico.validators.spec.ts`

---

## Entregables

- Implementación Angular
- Tests unitarios
- Documentación técnica

---

## Dependencias

### Previas
- Catálogos para selects
- Reglas de validación definidas

---

## Notas Técnicas

- No hardcodear catálogos
- No lógica de negocio en componentes UI
- Preparar estructura para pasos adicionales
- Formulario escalable

---

## Historial de Cambios

| Versión | Fecha | Autor | Cambios |
|-------|------|-------|--------|
| 1.1 | 2026-01-19 | Frontend | Adaptación desde HU UX/UI |
