
# HU-002: Implementación Frontend – Pantalla Planes de Vinculaciones

## Información General

**ID:** HU-002  
**Módulo:** G.vinculaciones  
**Tipo:** Desarrollo Frontend  
**Prioridad:** Media  
**Estimación:** 8 puntos  
**Sprint:** Por definir  

---

## Historia de Usuario

**Como** Desarrollador Frontend del equipo Atlantis Nexus  

**Quiero** implementar la pantalla de **Planes de Vinculaciones** utilizando Angular y Tailwind CSS  

**Para** permitir que los usuarios visualicen y seleccionen el tipo de plan (Básico o Complementario) de forma accesible, responsive y consistente con los lineamientos técnicos y visuales del proyecto

---

## Alcance de la Historia

Incluye:
- Implementación de la UI basada en diseño aprobado
- Comportamiento interactivo de selección de planes
- Navegación frontend según plan seleccionado
- Accesibilidad (WCAG 2.1 AA)
- Responsive design

No incluye:
- Definición de contenidos textuales finales
- Lógica de negocio backend
- Persistencia de datos
- Reglas de pricing o validaciones de dominio

---

## Descripción Técnica

### 1. Página Principal (Smart Component)

**Archivo:** `planes-vinculaciones-page.component.ts`

Responsabilidades:
- Renderizar el header y layout general
- Definir la lista de planes disponibles
- Manejar la navegación al seleccionar un plan
- Coordinar componentes presentacionales

---

### 2. Componentes Presentacionales (Dumb)

#### PlanCardComponent
**Archivo:** `plan-card.component.ts`

Responsabilidades:
- Renderizar la información visual del plan
- Manejar estados hover / focus / selected
- Emitir evento al seleccionar el plan

#### PlanFeatureItemComponent
**Archivo:** `plan-feature-item.component.ts`

Responsabilidades:
- Renderizar una característica con icono check
- Aplicar color según tipo de plan

---

## Accesibilidad (Obligatorio)

Las cards deben:
- Tener `role="button"` o usar elemento `<button>`
- Ser navegables por teclado (`tabindex="0"`)
- Responder a eventos de teclado (`Enter`)
- Mostrar estados `focus-visible`
- Incluir `aria-label` en iconos informativos

Cumple WCAG 2.1 nivel AA.

---

## Especificación Técnica

### Tecnologías
- Angular 20 (Standalone Components)
- ChangeDetectionStrategy.OnPush
- Angular Signals
- Tailwind CSS 4.x
- Angular Router

---

### Tipos de Datos

```ts
export type TipoPlan = 'BASICO' | 'COMPLEMENTARIO';

export interface PlanVinculacion {
  tipo: TipoPlan;
  titulo: string;
  descripcion: string;
  color: 'blue' | 'purple';
  icono: string;
  caracteristicas: string[];
}
```

---

### Inputs / Outputs

**PlanCardComponent**
```ts
plan = input.required<PlanVinculacion>();
seleccionado = input(false);
planSeleccionado = output<PlanVinculacion>();
```

---

### Estructura de Carpetas

```
modules/vinculaciones/
├── pages
│   └── home
│       ├── planes-vinculaciones-page.component.ts
│       └── components
│           ├── plan-card.component.ts
│           └── plan-feature-item.component.ts
└── shared
    └── types
        └── plan-vinculacion.types.ts
```

---

## UI Principal (Segun UX/UI)

### Header de la Pantalla
- Titulo: "Planes de Vinculaciones"
- Integracion con barra superior Atlantis Nexus (logo, ayuda, notificaciones)
- Integracion con menu lateral (Inicio, G.vinculaciones, Parametricas, Configuraciones, Salir)

---

### Cards de Planes

**Card Plan Basico**
- Icono usuario individual (azul)
  - Fondo: #DBEAFE, icono: #3B82F6
  - Tamano: 64px x 64px, forma circular
- Titulo: "Basico" (Roboto Bold, 24px, #111827)
- Descripcion: pendiente de contenido (Roboto Regular, 14px, #4B5563)
- Caracteristicas:
  - "Unico Integrante"
  - "Activo"
- Card:
  - Ancho 280px, padding 32px
  - Background #FFFFFF, border 1px #E5E7EB, radius 16px
  - Shadow: 0 4px 6px -1px rgba(0,0,0,0.1)
  - Hover: shadow-lg, scale(1.02)

**Card Plan Complementario**
- Icono usuarios multiples (morado)
  - Fondo: #F3E8FF, icono: #A855F7
  - Tamano: 64px x 64px, forma circular
- Titulo: "Complementario" (Roboto Bold, 24px, #111827)
- Descripcion: pendiente de contenido (Roboto Regular, 14px, #4B5563)
- Caracteristicas:
  - "Responsable del Plan"
  - "Agregar grupo familiar"
  - "Tarifa diferenciada producto aportes en grupo familiar"
- Card:
  - Ancho 280px, padding 32px
  - Background #FFFFFF, border 1px #E5E7EB, radius 16px
  - Shadow: 0 4px 6px -1px rgba(0,0,0,0.1)
  - Hover: shadow-lg, scale(1.02)

---

### Elementos de Caracteristicas (Checklist)

**Basico (Azul)**
- Icono check circular 24px
- Fondo: #DBEAFE, check: #2563EB

**Complementario (Morado)**
- Icono check circular 24px
- Fondo: #F3E8FF, check: #9333EA

**Texto**
- Roboto Regular, 14px, #374151
- Gap 12px con el icono

**Separadores**
- Linea horizontal 1px #E5E7EB
- Margin vertical 12px

---

### Disposicion de Cards
- Layout flex centrado horizontal, gap 32px
- Alineacion vertical centrada
- Responsive: < 768px cards apiladas, width 100%

---

## Comportamiento

### Interacciones
- Hover:
  - `scale(1.02)`
  - `shadow-lg`
- Click / Enter:
  - Emite evento de selección
  - Navega a `/vinculaciones/gestion?plan={tipo}`

### Responsive
- >= 768px: cards horizontales, gap 32px
- < 768px: cards apiladas verticalmente, width 100%

---

## Criterios de Aceptación – Frontend

### Funcionales
- [ ] Renderiza correctamente ambos planes
- [ ] Permite seleccionar un plan vía click o teclado
- [ ] Navega correctamente según el plan
- [ ] Responsive funcional en mobile y desktop

### Técnicos
- [ ] Componentes standalone
- [ ] Uso de signals
- [ ] OnPush habilitado
- [ ] Cumple lineamientos Atlantis Nexus

### Accesibilidad
- [ ] Navegación por teclado
- [ ] Focus visible
- [ ] Aria-labels presentes
- [ ] Contraste AA

---

## Pruebas

- Unit tests para:
  - Renderizado de cards
  - Emisión de evento de selección
  - Navegación
- Archivos:
  - `plan-card.component.spec.ts`
  - `planes-vinculaciones-page.component.spec.ts`

---

## Entregables

- Implementación Angular
- Tests unitarios
- Documentación técnica en Markdown

---

## Dependencias

### Previas
- Contenido final de descripciones
- Sistema de iconos definido
- Design System actualizado

---

## Notas Técnicas

- No usar CSS custom salvo excepciones (@apply)
- Evitar lógica de negocio en componentes presentacionales
- Preparar componentes para futuros planes

---

## Historial de Cambios

| Versión | Fecha | Autor | Cambios |
|-------|------|-------|--------|
| 1.1 | 2026-01-19 | Frontend | Adaptación desde UX/UI a implementación |
