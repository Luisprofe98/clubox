# Prompt para Codex: modulo cuotas y pagos preparado

## Objetivo
Dejar preparada una pantalla de cuotas y pagos sin integrar todavia pasarela real ni banco. La aplicacion debe soportar que cada club defina cuotas para jugadores, socios o formularios.

## Alcance MVP

Implementar una pantalla sencilla con:

- Listado de planes de cuota.
- Crear cuota.
- Editar cuota.
- Eliminar cuota.
- Estado visual de integracion pendiente.

No implementar cobros reales.
No almacenar tarjetas.
No llamar a APIs de pago.

## Campos de feePlan

- Nombre.
- Importe.
- Periodicidad.
- Tipo destinatario.
- Estado.

Periodicidad:

- unica
- mensual
- trimestral
- anual

Tipo destinatario:

- jugador
- socio
- formulario

Estados:

- activo
- inactivo

## Relacion con formularios

Al final de cada formulario puede existir `pagoConfig`:

- pagoActivo.
- feeId.
- pagoTipo.
- importe.

Si `pagoActivo` es true, mostrar bloque informativo al completar formulario:

- `Pago pendiente de integrar` warning.

## Relacion con contabilidad

Cuando en el futuro un pago se marque como pagado, debe poder generar un movement de tipo ingreso con clase `cuotasSocios` o `inscripciones`.

En MVP solo dejar el metodo preparado en feeService:

```js
export async function crearIngreso(pagoId) {}
```

El metodo debe lanzar warning o devolver estado pendiente hasta que pagos existan.

## Mensajes

- `Cuota guardada` succed.
- `Cuota eliminada` succed.
- `Pago online pendiente de configurar` warning.
- `Importe no valido` failed.

## Criterios de aceptacion

- Se puede crear un plan de cuota.
- Se puede listar y editar.
- Se muestra claramente que pagos reales estan pendientes.
- No hay iconos ni acentos en UI.
