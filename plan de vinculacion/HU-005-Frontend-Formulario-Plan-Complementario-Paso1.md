
# HU-005: Implementación Frontend – Formulario Plan Complementario (Paso 1)

## Información General

**ID:** HU-005  
**Módulo:** vinculaciones  
**Tipo:** Desarrollo Frontend  
**Prioridad:** Media  
**Estimación:** 13 puntos  
**Sprint:** Por definir  

---

## Historia de Usuario

**Como** Desarrollador Frontend del equipo Atlantis Nexus  

**Quiero** implementar el **Formulario Plan Complementario – Paso 1** como un formulario multipaso con campos específicos para el responsable del plan  

**Para** permitir el registro de una vinculación complementaria (grupal/familiar), capturando correctamente la información del responsable del plan y dejando preparada la navegación para agregar beneficiarios en pasos posteriores

---

## Alcance de la Historia

### Incluye
- Implementación del formulario Paso 1 (Plan Complementario)
- Captura de datos del responsable del plan
- Validaciones frontend en tiempo real
- Búsqueda opcional de asociado que presenta
- Stepper de 3 pasos
- Navegación al Paso 2
- Accesibilidad WCAG 2.1 AA
- Responsive design

### No incluye
- Implementación de Paso 2 y Paso 3
- Gestión de beneficiarios
- Persistencia backend
- Definición semántica final de campos “Value”
- Diseño UX/UI (ya aprobado)

---

## Descripción Técnica

### 1. Página (Smart Component)

**Archivo:** `plan-complementario-paso1-page.component.ts`

Responsabilidades:
- Inicializar el Reactive Form del Plan Complementario
- Gestionar estado del stepper (3 pasos)
- Validar campos del responsable
- Manejar navegación entre pasos
- Coordinar búsqueda de asociado que presenta

---

### 2. Componentes Presentacionales (Dumb)

- `plan-complementario-form.component.ts`

Responsabilidades:
- Renderizado visual
- Inputs / Outputs
- Sin lógica de negocio

---

## Accesibilidad (Obligatorio)

- Inputs con `<label>` asociado
- Campos requeridos con `aria-required="true"`
- Mensajes de error con `role="alert"`
- Orden lógico de tabulación
- Estados `focus-visible`
- Navegación completa por teclado
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

### Estructura del Formulario (Paso 1)

**Campos requeridos:**
- Tipo de identificación
- Primer apellido
- Primer nombre
- Fecha de nacimiento
- Email
- Value (campo izquierdo)
- Value (campo derecho)

**Campos opcionales:**
- Segundo apellido
- Segundo nombre
- Celular
- Asociado que presenta

---

### Validadores

```ts
soloNumeros
soloLetras
emailValido
celularColombia
mayorEdad
identificacionPorTipo
opcionRequerida
```

---

### Comportamiento

- Validaciones onBlur / onChange
- Botón Continuar habilitado solo si el formulario es válido
- Botón Limpiar con confirmación modal
- Navegación a `/vinculaciones/plan-complementario/paso-2`
- Persistencia temporal de datos del responsable

---

## Estructura de Carpetas

```
modules/vinculaciones/
├── pages/
│   └── plan-complementario/
│       ├── pages/
│       │   └── paso-1/
│       │       ├── plan-complementario-paso1.page.ts
│       │       ├── plan-complementario-paso1.page.html
│       │       └── plan-complementario-paso1.page.spec.ts
│       │
│       ├── services/
│       │   └── plan-complementario.state.ts
│       │
│       └── plan-complementario.routes.ts
```

---

## Criterios de Aceptación – Frontend

### Funcionales
- [ ] Renderiza todos los campos del Paso 1
- [ ] Aplica validaciones correctamente
- [ ] Permite buscar asociado opcionalmente
- [ ] Muestra stepper con 3 pasos (paso 1 activo)
- [ ] Navega al Paso 2 cuando el formulario es válido

### Técnicos
- [ ] Standalone Components
- [ ] Reactive Forms
- [ ] Validadores reutilizables
- [ ] OnPush habilitado
- [ ] Cumple lineamientos Atlantis Nexus

### Accesibilidad
- [ ] Labels visibles
- [ ] Errores accesibles
- [ ] Navegación por teclado
- [ ] Contraste AA

---

## Pruebas

- Tests unitarios:
  - Validadores personalizados
  - Estado de formulario válido / inválido
  - Navegación al Paso 2
- Archivos:
  - `plan-complementario-paso1-page.component.spec.ts`
  - `plan-complementario.validators.spec.ts`

---

## Entregables

- Implementación Angular Paso 1
- Tests unitarios
- Documentación técnica

---

## Dependencias

### Previas
- Catálogos para dropdowns
- API de búsqueda de asociados
- Definición funcional de campos “Value”

---

## Notas Técnicas

- Mantener diferencias visuales mediante tokens (morado)
- Reutilizar componentes del Plan Básico cuando sea posible
- Preparar estructura para pasos 2 y 3 (beneficiarios)
- Evitar lógica de negocio en UI

---

## Historial de Cambios

| Versión | Fecha | Autor | Cambios |
|-------|------|-------|--------|
| 1.1 | 2026-01-19 | Frontend | Adaptación desde HU UX/UI |
