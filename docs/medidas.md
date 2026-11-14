Circulaciones = COUNTROWS ( gold_fact_circulacion )

Puntualidad 5 min % =
DIVIDE ( CALCULATE ( [Circulaciones], gold_fact_circulacion[retraso_min] < 5 ), [Circulaciones] )

Puntualidad 15 min % =
DIVIDE ( CALCULATE ( [Circulaciones], gold_fact_circulacion[retraso_min] < 15 ), [Circulaciones] )

Minutos de retraso = SUM ( gold_fact_circulacion[retraso_min] )

Retraso medio trenes retrasados (min) =
CALCULATE ( AVERAGE ( gold_fact_circulacion[retraso_min] ), gold_fact_circulacion[retraso_min] >= 5 )

% minutos por infraestructura =
DIVIDE (
    CALCULATE ( [Minutos de retraso], gold_fact_circulacion[causa] = "Infraestructura" ),
    [Minutos de retraso]
)

Puntualidad 5 min % mes anterior =
CALCULATE ( [Puntualidad 5 min %], DATEADD ( gold_dim_fecha[fecha], -1, MONTH ) )

Llegadas por estación destino =
CALCULATE (
    [Circulaciones],
    USERELATIONSHIP ( gold_fact_circulacion[estacion_destino], gold_dim_estacion[stop_id] )
)