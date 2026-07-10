# Criterios de aceptacion y QA para Clubox

## QA general

- La aplicacion abre en `index.html` o en el comando definido por el repo.
- La navegacion es SPA y no recarga pagina.
- No hay errores de consola al navegar.
- No hay iconos ni emojis.
- No hay acentos en textos visibles.
- Bootstrap se usa para layout, tablas, forms, modals, tabs, cards y alerts.
- HTML, CSS y JS estan separados.
- Variables y funciones siguen lowerCamelCase y maximo dos palabras.

## QA datos

- Si no existe data local, se carga mock data.
- Al refrescar, los datos creados siguen en localStorage.
- No se pierden relaciones entre inscripciones, jugadores y equipos.
- Los importes mantienen dos decimales.

## QA formularios

- Crear formulario funciona.
- Editar formulario funciona.
- Anadir campos funciona.
- Reordenar campos funciona.
- Ver inscripciones funciona.
- Filtrar por estado funciona.
- Abrir ficha de inscripcion funciona.
- Aprobar inscripcion de deportista crea jugador.
- Rechazar inscripcion no crea jugador.

## QA gestion deportiva

- Listado de jugadores carga.
- Filtros por categoria, ano, estado y equipo funcionan.
- Ficha de jugador muestra datos e inscripciones.
- Crear equipo funciona.
- Asignar jugador a equipo funciona.
- Crear tecnico funciona.
- Asignar tecnico a equipo funciona.
- Historial de temporadas se puede visualizar.

## QA contabilidad

- Crear ingreso funciona.
- Crear gasto funciona.
- Editar movimiento funciona.
- Eliminar movimiento funciona.
- Ingresos aparecen en verde con signo +.
- Gastos aparecen en rojo con signo -.
- Filtros superiores funcionan.
- Orden reciente y antiguo funciona.
- Total ingresos es correcto.
- Total gastos es correcto.
- Resultado actual es correcto.
- PyG simplificada agrupa por partida.
- Exportaciones muestran warning si no estan implementadas.

## QA cuotas

- Crear cuota funciona.
- Editar cuota funciona.
- Eliminar cuota funciona.
- Pagos reales muestran warning de pendiente.

## QA responsive

Probar tamanos:

- Mobile 375 px.
- Tablet 768 px.
- Desktop 1280 px.

Requisitos:

- Navbar usable.
- Tablas con scroll horizontal si hace falta.
- Modals no se cortan.
- Botones visibles.

## QA manual recomendado

1. Crear formulario deportista.
2. Crear inscripcion recibida.
3. Aprobar inscripcion.
4. Ir a gestion deportiva.
5. Ver jugador generado.
6. Crear equipo.
7. Asignar jugador.
8. Crear ingreso por cuota.
9. Crear gasto de material.
10. Revisar resumen economico.

## Pendientes conocidos permitidos en MVP

- Google Cloud no conectado.
- Pagos reales no conectados.
- Exportacion Excel/PDF puede quedar en warning.
- Subida real de documentos puede quedar simulada.
- Firma digital no implementada.
- Comunicaciones automaticas no implementadas.
