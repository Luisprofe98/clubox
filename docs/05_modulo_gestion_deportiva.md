# Prompt para Codex: modulo gestion deportiva

## Objetivo
Implementa el modulo de gestion deportiva para centralizar jugadores, equipos, cuerpo tecnico e historial de temporadas.

## Pantallas internas

Usar tres tabs Bootstrap:

1. Jugadores.
2. Equipos.
3. Cuerpo tecnico.

## Tab Jugadores

### Listado
Mostrar tabla con:

- Nombre y apellidos.
- Ano nacimiento.
- Categoria.
- Equipos asignados.
- Estado.
- Acciones.

### Origen de jugadores
Los jugadores se crean automaticamente al aprobar una inscripcion de tipo deportista. Permitir edicion basica, pero marcar `inscriptionId` si procede.

### Filtros

- Categoria.
- Ano nacimiento.
- Estado.
- Equipo.
- Nombre.

Categorias iniciales:

- prebenjamin
- benjamin
- alevin
- infantil
- cadete
- juvenil
- senior

Estados:

- activo
- noActivo

### Ficha de jugador
Al abrir un jugador mostrar:

- Datos personales.
- Documentacion.
- Equipos asignados.
- Historial temporadas.
- Inscripciones asociadas.

Datos personales sugeridos:

- nombre
- apellidos
- dni
- fechaNacimiento
- direccion
- telefono
- email
- datosBanco
- tutorLegal

### Equipos asignados
Permitir:

- Anadir equipo mediante select.
- Eliminar asignacion.

Guardar relacion en `playerTeam`.

### Historial de temporadas
Mostrar registros:

- Temporada.
- Equipo.
- Categoria.

Permitir anadir registro manual.

## Tab Equipos

### Listado
Mostrar tabla con:

- Nombre equipo.
- Competicion.
- Entrenador principal.
- Numero jugadores.
- Acciones.

### Crear equipo
Boton `+ Nuevo equipo`.
Modal con:

- Nombre equipo.
- Competicion.
- Categoria.
- Entrenador principal.
- Estado.

El campo entrenador principal debe usar select desde staff.

### Ficha de equipo
Mostrar:

- Informacion general.
- Plantilla.
- Personal tecnico asignado.

En plantilla mostrar:

- Nombre y apellidos.
- Ano nacimiento.
- Estado.

Permitir:

- Anadir jugador.
- Eliminar jugador.

## Tab Cuerpo tecnico

### Listado
Mostrar tabla con:

- Nombre y apellidos.
- Cargo.
- Equipos asignados.
- Estado.
- Acciones.

### Crear miembro
Boton `+ Nuevo tecnico`.
Modal con:

- Nombre.
- Apellidos.
- DNI.
- Telefono.
- Email.
- Direccion.
- Cargo.
- Estado.

Cargos:

- entrenador
- segundoEntrenador
- delegado
- ayudante
- preparador
- fisio
- coordinador
- director
- otro

### Ficha de tecnico
Mostrar:

- Datos personales.
- Equipos asignados.

Permitir anadir o quitar equipo usando `staffTeam`.

## Relaciones

- player N team mediante playerTeam.
- staff N team mediante staffTeam.
- player N seasonHistory.
- inscription 1 player cuando se aprueba.

## Mensajes

Usar alertUtils:

- `Jugador actualizado` succed.
- `Equipo guardado` succed.
- `Tecnico guardado` succed.
- `Faltan campos obligatorios` failed.
- `El jugador ya esta asignado` warning.

## Datos mock iniciales

Crear:

- Dos equipos: Infantil A y Cadete B.
- Tres jugadores.
- Dos tecnicos.
- Asignaciones jugador equipo.
- Asignaciones tecnico equipo.

## Criterios de aceptacion

- Se ven jugadores creados desde inscripciones aprobadas.
- Se puede filtrar por categoria, ano, estado y equipo.
- Se puede abrir ficha de jugador.
- Se puede crear equipo y asignar jugadores.
- Se puede crear tecnico y asignarlo a equipos.
- No hay iconos ni acentos en UI.
