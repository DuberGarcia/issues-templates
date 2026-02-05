
# HU-002: Implementación Frontend – Pantalla Planes de Vinculaciones

## Historia de Usuario

**Como** Desarrollador Frontend del equipo Atlantis Nexus  

**Quiero** implementar la pantalla de "Planes de Vinculaciones" siguiendo el diseño UX/UI aprobado  

**Para** permitir a los usuarios visualizar y seleccionar un tipo de plan (Básico o Complementario) de forma clara, accesible y consistente con los lineamientos técnicos y visuales del proyecto

---

## Alcance Técnico

Esta historia cubre **exclusivamente la implementación frontend**, basada en los lineamientos de:
- Angular 20 (Standalone Components)
- Tailwind CSS 4.x
- Arquitectura Smart / Dumb Components
- Accesibilidad WCAG 2.1 AA
- Lineamientos Frontend Atlantis Nexus

No incluye definición de contenidos, reglas de negocio backend ni lógica de persistencia.

---

## Descripción Técnica

### 1. Estructura de Componentes

**Página (Smart Component):**
- `planes-vinculaciones-page.component.ts`
- Responsable de:
  - Renderizar layout general
  - Manejar navegación al seleccionar un plan
  - Integración con router

**Componentes Presentacionales (Dumb):**
- `plan-card.component.ts`
- `plan-feature-item.component.ts`

---

### 2. Comportamiento Esperado

#### Renderizado
- Se deben mostrar **dos cards** centradas horizontalmente:
  - Plan Básico
  - Plan Complementario

#### Interacción
- Hover:
  - `scale(1.02)`
  - `shadow-lg`
- Click:
  - Emite evento `planSeleccionado`
  - Navega a `/vinculaciones/gestion?plan={tipo}`

#### Responsive
- `<768px`: cards apiladas verticalmente
- `>=768px`: layout horizontal con gap de 32px

---

### 3. Accesibilidad

- Cards deben:
  - Tener `role="button"`
  - Ser navegables con teclado (`tabindex="0"`)
  - Responder a `Enter`
- Iconos con `aria-label`
- Estados `focus-visible` definidos

---

## Especificación de Implementación

### Tecnologías

- Angular 20 (Standalone)
- Signals para estado local
- ChangeDetectionStrategy.OnPush
- Tailwind CSS (sin CSS custom salvo excepciones)

---

### Inputs / Outputs

**PlanCardComponent**
```ts
plan = input.required<PlanVinculacion>();
seleccionado = input(false);
planSeleccionado = output<PlanVinculacion>();
```

---

### Tipos

```ts
export type TipoPlan = 'BASICO' | 'COMPLEMENTARIO';

export interface PlanVinculacion {
  tipo: TipoPlan;
  titulo: string;
  descripcion: string;
  icono: string;
  color: 'blue' | 'purple';
  caracteristicas: string[];
}
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

## Criterios de Aceptación – Frontend

### Funcionales

- [ ] Renderiza ambas cards correctamente
- [ ] Hover y click funcionan según lo definido
- [ ] Navegación correcta al seleccionar plan
- [ ] Responsive funcional en mobile y desktop

### Técnicos

- [ ] Componentes standalone
- [ ] OnPush habilitado
- [ ] Uso de signals
- [ ] Cumple nomenclatura y estructura Atlantis Nexus

### Accesibilidad

- [ ] Navegable por teclado
- [ ] Focus visible
- [ ] Aria-labels presentes
- [ ] Contraste AA

---

## Pruebas

- Tests unitarios para:
  - Renderizado de cards
  - Emisión de evento al click
  - Navegación
- Archivo:
  - `plan-card.component.spec.ts`

---

## Entregables

- Código Angular implementado
- Tests unitarios
- Storybook (opcional)
- Documentación técnica en Markdown

---

## Notas

- No hardcodear estilos fuera de Tailwind
- Preparar componente para futuros planes
- Evitar lógica de negocio en componentes presentacionales
