# arca — instrucciones para Codex

## Triggers — cuando aplicar estas instrucciones

Aplicar cuando el usuario mencione: dólar, tipo de cambio, oficial, blue, MEP, CCL, tarjeta, inflación, IPC, canasta básica, sueldo en dólares, economía argentina, convertir pesos, cuánto vale el dólar, precio del dólar.

---


# Skill: /arca

## Fecha actual

Antes de cualquier WebSearch que incluya año o mes, confirmá la fecha del sistema (`Bash: date` o contexto `currentDate`). Nunca asumas ni hardcodees el año — usá siempre el que reporta el sistema.

Consultá la economía argentina al instante. Hacé fetch a las APIs indicadas, procesá los datos y presentalos de forma clara.

## Comandos

### `/arca` o `/arca dolar`
Traé todos los tipos de cambio vigentes.

Fetch: `https://dolarapi.com/v1/dolares`

Presentá así:
```
💵 Dólar — [fecha hoy]

Oficial     $XX,XX  / $XX,XX
Blue        $XX,XX  / $XX,XX
MEP         $XX,XX  / $XX,XX
CCL         $XX,XX  / $XX,XX
Cripto      $XX,XX  / $XX,XX
Tarjeta     $XX,XX  / $XX,XX

(compra / venta)
```

Después de la tabla, una línea: brecha blue vs oficial en %.

---

### `/arca inflacion`
Último dato de inflación del INDEC.

Fetch: `https://apis.datos.gob.ar/series/api/series/?ids=148.3_INIVELNAL_DICI_M_26&limit=13&sort=desc&format=json`

Presentá así:
```
📈 Inflación — IPC Nacional

Último mes:     XX,X%  ([mes año])
Últimos 3m:     XX,X%
Últimos 12m:    XX,X%
Acumulado año:  XX,X%
```

Si podés calcular el acumulado del año con los datos disponibles, hacelo. Si no, aclaralo.

---

### `/arca sueldo [monto]`
Convertí un sueldo en pesos a su equivalente en distintos tipos de cambio.

Primero fetch dólar (igual que `/arca dolar`), luego calculá:

```
💼 Sueldo $[monto] ARS

Blue        u$s XXX
MEP         u$s XXX
CCL         u$s XXX
Oficial     u$s XXX
Tarjeta     u$s XXX
```

Al final agregá: "Canasta básica total: ~$XXX.XXX (INDEC [mes])" para dar contexto de poder adquisitivo.

Fetch canasta: `https://apis.datos.gob.ar/series/api/series/?ids=150.1_CSTA_BATAL_0_D_20&limit=1&sort=desc&format=json`

---

### `/arca canasta`
Valor actual de la canasta básica total e indigencia.

Fetch canasta total y alimentaria en una sola llamada (13 meses para calcular la variación interanual): `https://apis.datos.gob.ar/series/api/series/?ids=150.1_CSTA_BATAL_0_D_20,150.1_CSTA_BARIA_0_D_26&limit=13&sort=desc&format=json`

Cada fila de `data` es `[fecha, canasta total, canasta alimentaria]`. La total marca la línea de pobreza y la alimentaria la de indigencia.

Nota: son valores por adulto equivalente para GBA, la serie de referencia que publica el INDEC cada mes. Las series regionales (`444.1_CANASTA_*`) dejaron de actualizarse en diciembre de 2025: no usarlas. Aclarar en la respuesta que el valor es por adulto equivalente en GBA.

Presentá:
```
🛒 Canasta Básica — [mes año]

No pobreza:    $X.XXX.XXX
No indigencia: $XXX.XXX

Variación vs mes anterior:  +X,X%
Variación vs año anterior:  +XX,X%
```

---

### `/arca tarifas`
Info sobre tarifas de servicios públicos.

Buscá en la web: `tarifas servicios públicos Argentina [mes actual] [año actual]`

Presentá lo que encuentres de fuentes oficiales (ENRE, ENARGAS, Boletín Oficial) con fecha y fuente. Indicá claramente si los datos no son recientes.

---

## Manejo de errores

Si `dolarapi.com` no responde, usá como respaldo: `https://api.bluelytics.com.ar/v2/latest`

Si las APIs del INDEC no responden, buscá en la web con `site:indec.gob.ar [indicador]`.

Siempre mostrá fecha del dato y fuente.

Si el usuario escribe `/arca [otra cosa]`, interpretá la intención. Si no hay match, listá los comandos disponibles.

## Tono

Directo, sin comentario político ni económico. Datos, fuente y fecha. El usuario saca sus propias conclusiones.
