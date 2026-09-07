### Análisis de Datos y Creación de Dashboards ###
### Herramientas Utilizadas: Excel
### Contexto de la Simulación: Se me dio una base de datos con 1000 mediciones de una máquina de inspección de pasta de soldadura, las instrucciones fueron:
Estimado analista,
La próxima semana tenemos la visita de los auditores externos para nuestras certificaciones ISO y la revisión trimestral con los clientes del sector Automotriz y Médico.
Acabo de enviarte el archivo Flex_SMT_Process_Data.csv con la extracción de los últimos 1,000 lotes procesados en el área de impresión de pasta (SMT). He notado un incremento en nuestras mermas financieras y quejas de piso de producción, pero necesito que los datos hablen por sí solos.
Tu misión es diseccionar este archivo y presentarme un Dashboard de Calidad (Quality Dashboard) enfocado en Control Estadístico de Procesos (SPC).
Necesito que tu análisis responda las siguientes directrices y me entregues conclusiones ejecutivas sobre cada una:
1. Análisis de Capacidad del Proceso (Cp y Cpk) por Industria
Nuestros clientes de Automotive y Medical nos exigen por contrato mantener un Cpk mínimo de 1.33.
Tu tarea: Crea una tabla o gráfico que compare el Cpk promedio por familia de producto (Product_Family).
Pregunta a responder: ¿Estamos cumpliendo con el Cpk de 1.33 en los sectores críticos? ¿Qué está pasando con Consumer_Electronics, estamos sacrificando capacidad de proceso por velocidad?
2. Aislamiento de Variación (El problema de las Líneas SMT)
Sospecho fuertemente que una de nuestras impresoras de pasta está perdiendo calibración y nos está descentrando el proceso (la media se aleja del Target de 150 µm)
Tu tarea: Cruza la métrica de desviación estándar (Solder_Thickness_Std_um) y el Cpk contra las 3 líneas de producción (SMT_Line)
Pregunta a responder: ¿Hay alguna línea en particular que esté mostrando un desempeño estadístico inferior a las demás? De ser así, necesito los datos duros para justificar a Gerencia de Mantenimiento que paren esa máquina y la calibren.
3. Matriz de Causa-Efecto (Defectos y Costos)
Necesitamos entender el trade-off (el sacrificio) entre hacer las cosas rápido y hacerlas bien.
Tu tarea: Analiza la relación entre el tiempo de proceso (Process_Time_mins), la tasa de defectos (Defect_Rate_Pct) y el costo de producción (Production_Cost_USD).
Pregunta a responder: Cual es el punto en el que se encuentra el punto de equilibrio entre la velocidad y la efectividad del proceso?
Quiero saber si el departamento de Compras nos está afectando.
Tu tarea: Revisa cómo interactúa Supplier_Quality con la tasa de rechazo final (Status_Rejected).
4. Confianza en los Proveedores
Pregunta a responder: ¿A partir de qué calificación de calidad del proveedor el riesgo de que un lote se rechace por completo se vuelve inaceptable para la planta?
<img width="1477" height="486" alt="image" src="https://github.com/user-attachments/assets/32c1126c-fae8-43a0-9826-8d89b8e995d5" />

1.0 Análisis de Capacidad de Proceso 
<img width="1004" height="498" alt="image" src="https://github.com/user-attachments/assets/b23388ac-6b0c-4d18-977d-39a9fa1615f4" />
En base a esta tabla dinámica, podemos ver que tanto el sector automotriz cumple con el 1.33 de indice de cp, el cual es el estándar para procesos de producción.
Y el sector de Medicina cumple con ser mayor a el 2.00, que es el estándar para su sector, aunque con poco margen.
Sin embargo, el de electronica de consumo no cumple el estándar minimo de 1.33, quedandose muy por debajo.

<img width="596" height="351" alt="image" src="https://github.com/user-attachments/assets/f136e880-b344-446e-bd88-20c831089c48" />
Buscando la razón de esto, análice diferentes variables que pudieran afectar, y me di cuenta que es el único sector donde la calidad del proveedor baja del 90%, por 11 puntos,
y que tiene las operaciones con menos tiempo promedio por proceso, siendo de menos de 30 minutos.
En base a esto sugiero mejorar los proveedores del sector de electronica y aumentar el tiempo por proceso.

2.0 Aislamiento de Variación
Aquí llegue a la conclusión de que es muy probable que la impresora de la linea SMT-3 este perdiendo calibración, revisé las variables que pueden afectar a la calidad del proceso, y no parece haber razón aparente

<img width="856" height="106" alt="image" src="https://github.com/user-attachments/assets/0e61a371-7c56-4034-a079-12f9efe80388" />

3.0 Matriz de Causa-Efecto
En base a el análisis de datos llegué a la conclusión de que el equilibrio de eficiencia es que cada proceso dure 45 minutos o más, solo así se cumple con el indíce de cpk >=1.33, y si subimos más el tiempo de proceso
Simplemente se aumentan más los costos, a no ser que trabajemos en el sector de medicina, entonces cada proceso debe durar mínimo 60 minutos.

<img width="644" height="325" alt="image" src="https://github.com/user-attachments/assets/5e7afd4e-b971-4f8d-b8fd-0dca357ce8d4" />

4.0 Confianza en los Proveedores
Para que el riesgo de que un lote sea rechazado por completo se vuelva inaceptable, hace falta que el proveedor tenga una calificación menor a 90 puntos, donde el indice de process capability queda por debajo de los estandares
de 1.33

<img width="638" height="406" alt="image" src="https://github.com/user-attachments/assets/3806f3e9-0d75-43ed-a64d-92cf40a0b81c" />


además, al final agregué un dashboard interactivo para ver los KPIs

<img width="1764" height="938" alt="image" src="https://github.com/user-attachments/assets/87a2d0fb-eef3-47c6-900e-171d3d88a022" />

