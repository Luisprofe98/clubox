# Prompt para Codex: modulo formularios e inscripciones

## Objetivo
Implementa el modulo de formularios e inscripciones de Clubox. Debe permitir crear formularios personalizados, gestionar solicitudes recibidas y aprobar o rechazar inscripciones.

## Pantallas internas

El modulo tendra dos tabs Bootstrap:

1. Formularios.
2. Inscripciones recibidas.

## Tab Formularios

### Listado
Mostrar tabla con:

- Nombre formulario.
- Tipo formulario.
- Fecha creacion.
- Estado.
- Numero inscripciones.
- Acciones.

### Crear formulario
Crear boton de texto `+ Nuevo formulario`.
Al pulsarlo abrir modal Bootstrap con:

- Nombre formulario. Obligatorio.
- Tipo formulario. Obligatorio.
- Estado. Obligatorio.

Tipos:

- deportista
- socio
- torneo
- evento
- voluntario
- otro

Estados:

- activo
- inactivo

### Campos base
Todo formulario debe incluir por defecto:

- nombre
- apellidos
- fechaNacimiento
- dni

Estos campos son requeridos y no se eliminan en MVP.

### Biblioteca de campos
Permitir anadir campos desde una lista predefinida:

- padreNombre
- madreNombre
- tutorLegal
- telefono
- email
- direccion
- codigoPostal
- cuentaBanco
- iban
- domiciliacion
- clubOrigen
- observacionMedica
- alergias
- imagenDerechos
- datosProteccion

Los campos deben poder:

- Anadir.
- Eliminar si no son base.
- Reordenar con botones de texto `Subir` y `Bajar`.

No usar iconos para mover campos.

### Formulario publico
Cada formulario debe generar un `publicSlug` local. Preparar una vista simulada para completar el formulario.
No implementar publicacion real externa en MVP.

### Pago al final del formulario
Preparar seccion `pagoConfig` con:

- pagoActivo
- pagoTipo: unica, mensual
- importe
- proveedor: pendiente

No implementar pasarela real.
Mostrar aviso warning: `Pago online pendiente de configurar`.

## Tab Inscripciones recibidas

### Listado
Mostrar todas las solicitudes con:

- Fecha inscripcion.
- Nombre y apellidos.
- Tipo formulario.
- Estado inscripcion.
- Acciones.

### Estados

- recibida
- aprobada
- rechazada

### Vista por estados
Mostrar filtros rapidos o columnas por estado:

- recibida
- aprobada
- rechazada

### Ficha de inscripcion
Al abrir una inscripcion mostrar:

- Datos enviados.
- Documentacion adjunta.
- Estado actual.
- Observaciones internas.
- Acciones: Aprobar, Rechazar, Guardar nota.

### Documentacion obligatoria
Simular metadata para:

- dniAnverso
- dniReverso

No subir archivos reales si no hay backend. Si se implementa input file, guardar solo nombre, tipo y size.

## Filtros

Permitir filtrar inscripciones por:

- Estado: todas, recibida, aprobada, rechazada.
- Tipo formulario: deportista, socio, torneo, evento, voluntario.
- Fecha: hoy, semana, mes, rango.

## Regla clave: aprobar inscripcion

Cuando una inscripcion de tipo `deportista` pasa a `aprobada`:

1. Crear un player con los datos de la inscripcion.
2. Copiar datos principales: nombre, apellidos, dni, fechaNacimiento, telefono, email, direccion.
3. Calcular anoNacimiento desde fechaNacimiento.
4. Asignar estado `activo`.
5. Guardar `formId` e `inscriptionId` en player.
6. Guardar `jugadorId` en inscription.
7. Mostrar alert success usando estado `succed`.

Si ya existe `jugadorId`, no duplicar player.

## Mensajes de estado

Usar `alertUtils` con tipos:

- warning -> alert-warning.
- failed -> alert-danger.
- succed -> alert-success.

Textos sin acentos:

- `Formulario guardado`.
- `Inscripcion aprobada`.
- `Inscripcion rechazada`.
- `Faltan campos obligatorios`.
- `Pago online pendiente de configurar`.

## Datos mock iniciales

Crear al menos:

- Formulario `Inscripcion Temporada 2026 2027` tipo deportista activo.
- Formulario `Campus Verano` tipo evento activo.
- Tres inscripciones: una recibida, una aprobada, una rechazada.

## Criterios de aceptacion

- Se puede crear un formulario.
- Se pueden anadir y ordenar campos.
- Se puede ver listado de inscripciones.
- Se puede filtrar por estado.
- Se puede aprobar una inscripcion y comprobar que crea un jugador.
- No hay iconos ni acentos en UI.
