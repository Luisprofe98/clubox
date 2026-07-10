# Modelo de datos preparado para Google Cloud
## Objetivo
Definir entidades y relaciones para que la SPA funcione con localStorage ahora y pueda migrar a Google Cloud despues.
## Decision temporal
Mientras Google Cloud no este creado, usar `localProvider.js`. No acoplar la UI a localStorage.
## Campos base comunes
Todas las entidades deben tener:
```js
{
  id: "uuid",
  clubId: "club_demo",
  createdAt: "2026-01-01T10:00:00.000Z",
  updatedAt: "2026-01-01T10:00:00.000Z"
}
```
## Entidades principales
### club
Representa un club cliente.
Campos:
- id
- nombre
- estado
- colorPrimario
- colorSecundario
### form
Formulario creado por el club.
Campos:
- id
- clubId
- nombre
- tipo
- estado
- fechaAlta
- campoLista
- pagoConfig
- publicSlug
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
### formField
Campo configurable de formulario.
Campos:
- id
- formId
- nombre
- tipo
- requerido
- orden
- opciones
Tipos sugeridos:
- text
- number
- date
- select
- checkbox
- file
- textarea
- iban
- email
- phone
### inscription
Solicitud enviada desde un formulario.
Campos:
- id
- clubId
- formId
- tipo
- fechaAlta
- estado
- datoForm
- docLista
- notaInterna
- jugadorId
Estados:
- recibida
- aprobada
- rechazada
Regla:
- Si una inscription de tipo deportista pasa a aprobada, crear player si no existe y vincular `jugadorId`.
### document
Metadata de documentos adjuntos.
Campos:
- id
- clubId
- ownerType
- ownerId
- nombre
- tipo
- url
- estado
Documentos minimos:
- dniAnverso
- dniReverso
### player
Jugador generado desde una inscripcion aprobada o creado manualmente si se permite en fase futura.
Campos:
- id
- clubId
- nombre
- apellidos
- dni
- fechaNacimiento
- anoNacimiento
- categoria
- estado
- fechaAlta
- datoExtra
- formId
- inscriptionId
Estados:
- activo
- noActivo
### team
Equipo o grupo de trabajo.
Campos:
- id
- clubId
- nombre
- competicion
- categoria
- staffId
- estado
### staff
Miembro del cuerpo tecnico.
Campos:
- id
- clubId
- nombre
- apellidos
- dni
- telefono
- email
- direccion
- cargo
- estado
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
### playerTeam
Tabla intermedia para jugador y equipo.
Campos:
- id
- clubId
- playerId
- teamId
- fechaInicio
- fechaFin
- estado
Regla:
- Un jugador puede estar en varios equipos.
- Un equipo puede tener varios jugadores.
### staffTeam
Tabla intermedia para tecnico y equipo.
Campos:
- id
- clubId
- staffId
- teamId
- cargo
- fechaInicio
- fechaFin
- estado
Regla:
- Un tecnico puede estar en varios equipos.
### seasonHistory
Historial de temporadas del jugador.
Campos:
- id
- clubId
- playerId
- temporada
- teamId
- categoria
### budgetItem
Partida presupuestaria.
Campos:
- id
- clubId
- nombre
- tipo
- estado
Tipos:
- ingreso
- gasto
### movement
Movimiento economico.
Campos:
- id
- clubId
- tipo
- fecha
- importe
- clase
- concepto
- medioPago
- playerId
- budgetId
- temporada
Tipos:
- ingreso
- gasto
Medios:
- banco
- efectivo
### feePlan
Plan de cuota para jugadores o socios.
Campos:
- id
- clubId
- nombre
- importe
- periodicidad
- estado
Periodicidad:
- unica
- mensual
- trimestral
- anual
### payment
Pago registrado o futuro pago online.
Campos:
- id
- clubId
- ownerType
- ownerId
- importe
- estado
- proveedor
- fechaPago
- referencia
Estados:
- pendiente
- pagado
- fallido
## Relacion general entre modulos
```text
form -> N inscription
inscription aprobada -> 1 player
player -> N playerTeam -> N team
staff -> N staffTeam -> N team
player -> N seasonHistory
budgetItem -> N movement
player -> N movement opcional
feePlan -> N payment futuro
```
## Colecciones si se usa Firestore
```text
clubs/{clubId}/forms/{formId}
clubs/{clubId}/inscriptions/{inscriptionId}
clubs/{clubId}/players/{playerId}
clubs/{clubId}/teams/{teamId}
clubs/{clubId}/staff/{staffId}
clubs/{clubId}/playerTeams/{playerTeamId}
clubs/{clubId}/staffTeams/{staffTeamId}
clubs/{clubId}/seasonHistory/{seasonId}
clubs/{clubId}/budgetItems/{budgetId}
clubs/{clubId}/movements/{movementId}
clubs/{clubId}/feePlans/{feeId}
clubs/{clubId}/payments/{paymentId}
```
## Validaciones minimas
- No crear inscripcion sin formId.
- No aprobar inscripcion de deportista sin nombre, apellidos, fechaNacimiento y dni.
- No crear movimiento sin tipo, fecha, importe y clase.
- No crear equipo sin nombre.
- No crear staff sin nombre, apellidos y cargo.
- No guardar importe negativo. El signo lo determina `tipo`.
