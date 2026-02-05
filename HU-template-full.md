# [HU-XXX] Título claro orientado a valor

## 📋 Historia

**Como** [rol]  
**Quiero** [acción]  
**Para** [beneficio]

Objetivo usuario: [qué gana]  
Objetivo negocio: [qué aporta]

---

## ✅ Criterios de Aceptación

> Condiciones para considerar la historia como completada

### Funcionalidad
- [ ] Permite [acción principal]
- [ ] Ejecuta [proceso esperado]
- [ ] Bloquea acciones inválidas

### UI / Experiencia
- [ ] Muestra estados claros (loading, error, éxito)
- [ ] Da feedback inmediato

### Validación
- [ ] No permite continuar incompleto
- [ ] Valida contra backend
- [ ] Maneja errores correctamente

### Compatibilidad
- [ ] Funciona en desktop
- [ ] Funciona en móvil
- [ ] Compatible con navegadores soportados 

---

## 🔁 Flujos y Escenarios

> Describen el comportamiento, NO son requisitos de aceptación

### Flujo principal
1. Usuario ingresa dato
2. Sistema valida
3. Carga información
4. Usuario continúa

### Casos alternos
- Si no existe → mensaje
- Si falla API → reintento
- Si sesión expira → login

### Escenarios (opcional – BDD)

```gherkin
Given usuario autenticado
When realiza la acción principal
Then obtiene el resultado esperado
```

---

## 🎨 Diseño & UX

Mockup: [Figma / Link]  

Layout:
- Componentes principales
- Organización visual

Interacción:
- Hover / Focus
- Mensajes
- Animaciones

Estados visuales:
- Inicial
- Cargando
- Error
- Confirmación

Responsive:
- Desktop: [comportamiento]
- Mobile: [comportamiento]

---

## 🔌 Integración API

Endpoint: `METHOD /ruta`  
Auth: Sí / No  
Timeout esperado: XX ms  

Respuestas:
- 200: OK
- 4xx: Error usuario
- 5xx: Error sistema

Dependencias:
- Servicio X
- Catálogo Y

---

## 📋 Reglas de Negocio

1. Regla principal
2. Restricción secundaria
3. Excepciones

---

## ⚠️ Consideraciones Técnicas

> Guías, NO implementación

- Manejo de sesión
- Performance
- Seguridad
- Escalabilidad
- Logging

---

## 🔗 Dependencias

- Depende de: HU-XXX
- Bloquea: HU-YYY

---

## ✅ Definition of Done (dependiendo de la historia)

### Funcional
- [ ] Criterios cumplidos
- [ ] Flujos validados

### UX
- [ ] Diseño aprobado
- [ ] Responsive OK

### Calidad
- [ ] Code review (si aplica)
- [ ] Tests passing
- [ ] Sin warnings

### Documentación
- [ ] Actualizada
- [ ] Comentarios clave

---

## 📝 Notas

Decisiones:
- [Decisión 1]
- [Decisión 2]

Riesgos:
- [Riesgo 1]
- [Riesgo 2]

Referencias:
- [Links]

---
