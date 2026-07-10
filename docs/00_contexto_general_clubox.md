# Contexto general para Codex: Clubox

## Rol de Codex
Actua como arquitecto frontend y desarrollador senior. Implementa Clubox como una aplicacion web para gestion de clubes deportivos. La aplicacion debe ser sencilla, rapida e intuitiva para directivos de clubes, no para socios finales.

## Objetivo del producto
Clubox centraliza los procesos basicos de un club deportivo:

1. Formularios e inscripciones.
2. Gestion deportiva.
3. Contabilidad basica de ingresos y gastos.
4. Cuotas y pagos como integracion preparada para una fase posterior.

## Alcance inicial
Construir una Single Page Application con Bootstrap y programacion modular. Debe poder ejecutarse sin backend real mientras la base de datos de Google Cloud no este disponible.

La primera version debe incluir:

- Navegacion interna sin recargar pagina.
- Modulos separados por archivos.
- Datos persistidos temporalmente con localStorage o mock provider.
- Capa de acceso a datos preparada para cambiar a Google Cloud.
- HTML, CSS y JS separados.
- Sin iconos, sin emojis y sin librerias de iconos.
- Textos visibles sin acentos.

## Modulos principales

### Formularios e inscripciones
Permite crear formularios editables, personalizar campos, recibir solicitudes, revisar documentacion, aprobar o rechazar inscripciones y preparar la generacion automatica de jugadores.

### Gestion deportiva
Permite administrar jugadores, equipos, cuerpo tecnico, asignaciones y temporadas. Los jugadores se crean automaticamente cuando una inscripcion de tipo deportista se aprueba.

### Contabilidad basica
Permite registrar ingresos y gastos, filtrar movimientos, ver libro diario, resumen economico, cuenta de resultados simplificada y preparar exportaciones.

### Cuotas y pagos
Debe quedar preparado a nivel de estructura, aunque la integracion real con pasarela de pago y banco no se implementara hasta que el stack backend este definido.

## Restricciones obligatorias

- Usar Bootstrap 5 para estructura, grid, tablas, modales, formularios, cards, navs y alerts.
- Usar una SPA modular en JavaScript.
- No usar frameworks pesados salvo que el repositorio ya los use.
- Separar archivos: HTML, CSS y JS.
- Variables y funciones en lowerCamelCase, maximo dos palabras descriptivas.
- Ejemplos validos: jugadorLista, equipoActivo, formEstado, movFiltro, guardarMov, cargarEquipo.
- Ejemplos no validos: listaCompletaDeJugadores, renderAccountingSummary, movimientoEconomicoActual.
- Colores principales basados en burdeo, blanco y negro.
- No usar iconos ni emojis.
- No usar acentos en textos visibles, variables, ids, clases ni nombres de archivo.
- La base de datos estara en Google Cloud, pero aun no existe. Implementa una capa dataProvider para desacoplar la UI del origen de datos.

## Paleta inicial
Usar variables CSS globales:

```css
:root {
  --clubox-primary: #6e1028;
  --clubox-secondary: #9c1b3d;
  --clubox-dark: #111111;
  --clubox-light: #ffffff;
  --clubox-muted: #f5f2f3;
  --clubox-border: #e6dde0;
  --clubox-success: #198754;
  --clubox-warning: #ffc107;
  --clubox-failed: #dc3545;
}
```

## Estilo visual

- Look limpio, profesional y tecnologico.
- Mucho espacio en blanco.
- Cards con bordes suaves.
- Tablas claras y faciles de filtrar.
- Botones principales en burdeo.
- Estados success, warning y failed con Bootstrap.
- El boton de alta puede ser el caracter "+" como texto, no como icono.

## Prioridad de implementacion

1. Crear estructura SPA y router interno.
2. Crear capa dataProvider con mock/localStorage.
3. Crear modulo de formularios.
4. Crear flujo aprobar inscripcion -> crear jugador.
5. Crear gestion deportiva.
6. Crear contabilidad basica.
7. Crear resumen economico y filtros.
8. Dejar stubs claros para Google Cloud, pagos, exportaciones y documentos.
