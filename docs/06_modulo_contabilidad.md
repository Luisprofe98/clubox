# Prompt para Codex: modulo contabilidad basica

## Objetivo
Implementa un modulo de contabilidad simplificada para clubes deportivos. No es contabilidad oficial completa. Debe servir para registrar y consultar ingresos y gastos de forma sencilla.

## Pantallas internas

Usar dos tabs Bootstrap:

1. Registro movimientos.
2. Resumen economico.

## Tab Registro movimientos

### Boton principal
Crear boton `+ Nuevo movimiento`.
Al pulsarlo abrir modal Bootstrap.

### Formulario movimiento
Campos:

- Tipo movimiento. Obligatorio. Select: ingreso, gasto.
- Fecha. Obligatorio. Por defecto hoy.
- Importe. Obligatorio. Numero positivo con dos decimales.
- Clase. Obligatorio. Select dependiente del tipo.
- Concepto. Opcional. Texto libre.
- Medio pago. Obligatorio. Select: banco, efectivo.
- Jugador. Opcional. Select preparado para relacion futura.

### Clases de ingresos

- cuotasSocios
- inscripciones
- patrocinios
- subvenciones
- ventaMaterial
- otrosIngresos

### Clases de gastos

- materialDeportivo
- arbitrajes
- licencias
- cambioPartido
- alquilerInstalaciones
- pagoEntrenadores
- transporte
- otrosGastos

### Libro diario
Debajo del boton mostrar tabla cronologica con:

- Fecha.
- Tipo.
- Clase.
- Importe.
- Concepto.
- Medio pago.
- Acciones.

Reglas visuales:

- Ingresos en verde con signo +.
- Gastos en rojo con signo -.
- Mas reciente primero por defecto.

### Acciones
Permitir:

- Editar movimiento.
- Eliminar movimiento.

Al editar o eliminar recalcular resumen automaticamente.

## Filtros

Filtros por columnas:

- Fecha.
- Tipo.
- Clase.
- Importe.
- Concepto.
- Medio pago.

Filtros superiores:

- Temporada.
- Mes actual.
- Trimestre actual.
- Tipo: todos, ingreso, gasto.
- Partida presupuestaria.

Orden:

- reciente.
- antiguo.

## Tab Resumen economico

### Cards superiores
Mostrar tres cards:

- Total ingresos.
- Total gastos.
- Resultado actual.

Calculos:

```text
totalIngresos = suma importes donde tipo = ingreso
totalGastos = suma importes donde tipo = gasto
resultadoActual = totalIngresos - totalGastos
```

Regla visual:

- Resultado positivo en verde.
- Resultado negativo en rojo.

### Cuenta de resultados simplificada
Mostrar dos columnas o dos tablas:

1. Ingresos por partida.
2. Gastos por partida.

Cada tabla debe agrupar por clase y sumar importes.

Ejemplo de estructura:

```text
Ingresos
Cuotas socios: 6000 EUR
Inscripciones: 2500 EUR
Total ingresos: 8500 EUR

Gastos
Material deportivo: 2000 EUR
Arbitrajes: 1500 EUR
Total gastos: 3500 EUR

Resultado final: 5000 EUR
```

## Exportaciones
Preparar botones:

- Exportar Excel.
- Exportar PDF.
- Exportar filtrados.
- Importar plantilla.

En MVP pueden mostrar warning `Exportacion pendiente de conectar` si no se implementan librerias.
No introducir dependencias pesadas sin revisar el repositorio.

## Importes

- Guardar numeros positivos.
- Formatear con dos decimales.
- Mostrar `EUR`.
- El signo se calcula por tipo.

## Mensajes

Usar alertUtils:

- `Movimiento guardado` succed.
- `Movimiento eliminado` succed.
- `Faltan campos obligatorios` failed.
- `Importe no valido` failed.
- `Exportacion pendiente de conectar` warning.

## Datos mock iniciales

Crear movimientos de ejemplo:

- ingreso cuotasSocios 150 banco.
- gasto materialDeportivo 80 efectivo.
- ingreso patrocinios 500 banco.
- gasto arbitrajes 120 banco.

## Criterios de aceptacion

- Se puede crear ingreso y gasto.
- Los ingresos aparecen verdes con signo +.
- Los gastos aparecen rojos con signo -.
- Se puede filtrar por tipo, clase y fecha.
- Se puede editar y eliminar.
- El resumen se recalcula automaticamente.
- La PyG simplificada agrupa por partida.
- No hay iconos ni acentos en UI.
