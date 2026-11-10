# Revisión de coherencia: Trabajo de grado (asistencia antifraude)

Revisado el 9 de noviembre de 2026. Se compararon tres cosas:

1. `Trabajo de grado.docx` (carpeta Trabajo). Es la misma versión que está cargada en el cuaderno.
2. Las 42 fuentes del cuaderno de NotebookLM **TRABAJO DE GRADO**, incluida la plantilla `Copia de Formato Trabajo de Grado FCBI` y las clases del Seminario de Investigación.
3. Los 40 patrones de la skill **humanizalo**, adaptados a redacción académica (ver sección 6).

No se modificó el documento. Cada punto indica **dónde** está el problema, **qué** está mal y **qué** poner en su lugar.

Prioridad:
- 🔴 = lo nota un jurado y puede costar la aprobación.
- 🟠 = incoherencia visible.
- 🟡 = forma o estilo.

---

## 1. Resumen del estado

| Aspecto | Estado |
|---|---|
| Estructura general | Completa hasta el Capítulo 9; faltan Conclusiones, Recomendaciones y Anexos |
| Datos del Objetivo 1 (diagnóstico) | **Vacíos**: Tabla 2 sin datos, Figura 2 sin gráfica, 7 marcadores `(PENDIENTE)` |
| Coherencia entre capítulos | **Baja en lo técnico**: el stack, el número de objetivos, el IMEI, el tiempo de rotación del QR y FaceAPI cambian según el capítulo |
| Citas frente a fuentes | **Varias citas mal atribuidas y referencias con autores o revistas que no coinciden con el PDF real** |
| Cálculos | 3 errores aritméticos (Tabla 12 y Marco contextual) |
| Usabilidad (parte del Objetivo 3) | Prometida en el resumen, el objetivo y la metodología, **pero no se presenta ningún resultado** |

---

## 2. Incoherencias internas (el documento se contradice)

### 2.1 🔴 Número de objetivos específicos: 3 o 4

El trabajo tiene **3 objetivos específicos** y 3 capítulos de desarrollo, pero varias secciones hablan de 4:

| Ubicación | Dice | Cambiar a |
|---|---|---|
| Introducción, párrafo de metodología | "El desarrollo se dividió en cuatro etapas vinculadas a los objetivos específicos" | Tres etapas: diagnóstico, diseño y construcción, validación |
| 5.1.2 (final) | "da respuesta al segundo y tercer objetivo" | "da respuesta al segundo objetivo" |
| 5.1.3 (final) | "fundamental para el cuarto objetivo específico" | "tercer objetivo específico" |
| 6.2 | "los cuatro objetivos específicos"; "fase final del objetivo 4"; "Objetivos 2, 3 y 4" | tres objetivos; "objetivo 3"; "Objetivos 2 y 3" |
| 6.3 | "los cuatro objetivos específicos" | tres |
| Tabla 1 | Filas "Objetivo 3: Construir…" y "Objetivo 4: Validar…" | Unir las filas 2 y 3 en "Objetivo 2: Diseñar e implementar…" y renombrar la fila 4 como "Objetivo 3" |
| 9.4 | "Un componente central del objetivo 4" | "del objetivo 3" |

### 2.2 🔴 Stack tecnológico distinto según el capítulo

El Capítulo 8 describe lo que realmente se construyó. Las secciones anteriores describen otra cosa:

| Ubicación | Dice | Realidad (Cap. 8) | Acción |
|---|---|---|---|
| Introducción, 6.3 (fuentes secundarias), Tabla 1 (fila Obj. 3) | Redis y Docker | 8.1 dice que **se eliminó Redis** y que las sesiones van en PostgreSQL. Docker no vuelve a aparecer | Quitar Redis en todas partes. Quitar Docker, o describir en 8.6 cómo se usó |
| Introducción | Frontend: "Vue.js 3, Tailwind CSS y Axios" | Además hay una **app móvil en React Native + Expo** | Mencionar la app móvil en la Introducción |
| 5.4, Ley 1273 | "PostgreSQL/MySQL" | Solo PostgreSQL 16 | Dejar solo PostgreSQL |
| 5.4, Ley 2502 | Prueba de vida con "FaceAPI.js" | **TensorFlow Lite + MobileFaceNet** en el celular | Cambiar a TensorFlow Lite/MobileFaceNet. FaceAPI.js solo aparece en Cano-Perfecto |
| Introducción | "arquitectura hexagonal" | 8.1 dice "cliente-servidor desacoplada"; la Figura 3 dice "arquitectura desacoplada" | Elegir un nombre. Si es hexagonal, nombrar los puertos y adaptadores en la Figura 3 |
| Resumen | "arquitectura de software relacional" | No es un término correcto | "arquitectura cliente-servidor con base de datos relacional" |

### 2.3 🔴 Identificación del dispositivo: IMEI o huella SHA-256

- 7.1 ("IMEI/Token") y la Tabla 1 ("IMEI") dicen que se usa el **IMEI**.
- 8.4.1 dice explícitamente que **no** se usa el IMEI, sino una huella SHA-256 del dispositivo.
- 5.2.5 y el glosario hablan de "identificadores únicos de hardware".

**Acción:** unificar como "huella digital del dispositivo (*device fingerprint*) mediante hash SHA-256" y redefinir 5.2.5 con esa idea. Corregir también 8.4.1, que dice "huella digital **cifrada** SHA-256": SHA-256 es una función hash, no cifrado. Debe decir "huella generada con la función hash SHA-256".

Explicar además qué datos alimentan el hash (por ejemplo, ID de instalación, modelo, versión del sistema operativo). Sin eso, un jurado preguntará si el estudiante puede reinstalar la app para obtener una huella nueva.

En la Tabla 4, "captura de huella digital del dispositivo" se puede confundir con una huella dactilar. Escribir "huella del dispositivo (device fingerprint)".

### 2.4 🔴 Rotación del código QR: 5 o 10 segundos

| Ubicación | Valor |
|---|---|
| 8.7 | rota "cada 5 segundos" con 3 s de tolerancia |
| Tabla 10 | "Rotación automática cada 10s con búfer de 3s" |
| Tabla 12 | "QR vencido (> 10 segundos)" |

**Acción:** revisar el código, dejar un solo valor y usarlo en las tres partes.

### 2.5 🔴 La ruta no biométrica cuando el docente exige biometría

- La Tabla 4 dice que la ruta no biométrica "es la ruta por defecto".
- En la Tabla 8 (paso 4), si `biometric_required = true` y el estudiante no tiene plantilla, la API responde **428** y abre la cámara.
- 8.9 dice que la ruta alternativa aplica "cuando un estudiante decide no registrar su rostro **o** la clase no requiere biometría".

**Hueco:** no se explica qué pasa cuando el docente **sí** exige biometría y el estudiante **no** autorizó su rostro. Este es justo el caso que exige la Ley 1581 (Art. 6) y el Decreto 1377 (Art. 6: "ninguna actividad podrá condicionarse a que el Titular suministre datos personales sensibles"). La Tabla 13 dice "activable con un clic", pero el flujo de la Tabla 8 no lo muestra.

**Acción:** añadir un paso a la Tabla 8 o un párrafo en 8.9. Ejemplo: "Si el estudiante no otorgó autorización biométrica, la API omite la verificación facial aunque `biometric_required` esté activo y registra el marcado con `method = alternativa`". Ajustarlo a lo que haga el código.

La Tabla 8 también mezcla **registro** de plantilla y **verificación**. El paso 4 dice "no hay biometría previa" y el paso 6 compara "contra la plantilla". Si no hay plantilla previa, no hay con qué comparar. Separar el enrolamiento (endpoint `/biometrics/template`) del marcado.

### 2.6 🟠 La prueba de vida promete más de lo que hace

- El glosario y 5.2.3 dicen que la prueba de vida "verifica la **tridimensionalidad**".
- La sección de la Ley 2502 dice que es "activa **y pasiva**" y que resiste "rostros sintéticos creados con IA".
- Lo implementado (8.9) es un **reto activo de gesto** (parpadear o sonreír). Eso no mide profundidad 3D ni detecta *deepfakes* de forma comprobada.

**Acción:** describirla como "prueba de vida activa por reto de gesto aleatorio". Pasar la detección pasiva y la resistencia a IA a **Limitaciones**, y después a Recomendaciones.

### 2.7 🟠 Tiempos del pase de lista manual: 15-20 o 20 minutos

- El resumen y el abstract dicen "de veinte minutos a menos de cinco".
- La Introducción, 2.5 y 5.3.3 dicen "15 a 20 minutos".
- El Capítulo 7 tiene el valor medido **pendiente**.

**Acción:** cuando tengan el dato medido del Objetivo 1, usar ese número en todo el documento: resumen, abstract, 2.5, 5.3.3, 6.2 y 9.2. Hoy "15-20 minutos" es una cifra sin cita. Si viene de la literatura, citarla; si no, quitarla.

### 2.8 🟠 "Elimina" o "99,4%"

- El resumen dice "elimina la suplantación".
- 9.3 dice "erradicando por completo".
- 9.4 dice "logra eliminar la suplantación con un 99.4% de efectividad", que se contradice a sí mismo.
- Las pruebas fueron **simulaciones hechas por ustedes**, no fraude real observado.

**Acción:** escribir "bloqueó el 99,3% de los 145 intentos de fraude simulados" (ver 3.1). No usar "elimina" ni "erradica".

### 2.9 🟠 Alerta de "deserción" o de pérdida de materia por fallas

8.10 calcula "porcentaje de faltas → alerta de **pérdida de materia**". El título y la Figura 10 la llaman alerta de **deserción**. No son lo mismo.

**Acción:**
1. Llamarla "alerta temprana por inasistencia (riesgo de pérdida de asignatura)", o explicar por qué se usa como indicador de deserción y citar una fuente.
2. Indicar el **umbral de faltas** que usa el sistema y de dónde sale (Reglamento Estudiantil de Unicatólica, artículo X). Hoy dice "porcentaje máximo de faltas" sin número.

### 2.10 🟡 Otras inconsistencias menores

- 8.3 dice "13 tablas", pero la Tabla 5 muestra 10. Aclarar "las 10 principales de las 13" o nombrar las 3 que faltan.
- 8.5 menciona los "Módulos M3 y M4", pero la Tabla 4 no tiene códigos. Añadir la columna de código M1-M6 a la Tabla 4.
- 8.5 dice que el diseño "demostró" factibilidad. En la etapa de diseño todavía no se demuestra nada; usar "permitió definir" y dejar "demostró" para el Capítulo 9.
- 8.10 cierra con "la plataforma 100% lista" y la Tabla 10 repite "100% Codificado/Funcional". Cambiar a "Implementado y probado en entorno de desarrollo".
- La Tabla 5 usa el estado `suplanted` (está en el código; si se cita, explicarlo como "suplantación detectada"). Marcar fuera de la geocerca **no es suplantación**. Explicar por qué se guarda con ese estado, o diferenciar `out_of_range`.
- El Capítulo 7 menciona "el sistema institucional **Banner**", que no aparece en ningún otro lugar. Presentarlo en el Marco contextual (5.3.2).
- El Capítulo 7 compara el resultado con la literatura ("Esta cifra supera…") **antes de tener la cifra**. Redactar la comparación solo cuando tengan el dato real; si su porcentaje sale menor que 35,4%, el párrafo actual quedaría falso.

---

## 3. Errores de cálculo

### 3.1 🔴 Tabla 12 (pruebas antifraude)

| Fila | En el documento | Correcto |
|---|---|---|
| Foto impresa / pantalla | 14 de 15 = **97,1%** | 14 / 15 = **93,3%** |
| Promedio global | 144 de 145 = **99,4%** | 144 / 145 = **99,3%** (el promedio simple de las 5 tasas da 98,7%; indicar cuál se usa) |

**También en la Tabla 12:**
- En 4 filas falta el valor de la columna "Intentos bloqueados", así que las columnas quedan corridas. Llenar 50, 40, 30 y 10.
- La fila 2 dice "> 20 metro". Corregir a "> 20 metros" y explicar en el Capítulo 8 que el radio de la geocerca es de 20 m.
- El texto de 9.3 lista 5 escenarios: captura de pantalla, fuera del aula, foto impresa, mismo celular y **vencimiento del QR**. La tabla trae otros 5: une captura y vencimiento, y agrega "vector alterado". Hacer que coincidan.
- "Suplantación facial con foto impresa / pantalla (Sin prueba de vida)" no se entiende: ¿se probó con la prueba de vida desactivada? Aclararlo.
- Corregir 99.4 → 99,3 también en 9.3, 9.4 y, después, en el resumen.

### 3.2 🔴 Marco contextual 5.3.3: horas perdidas por semana

"15 a 20 minutos por sesión × 4 asignaturas por semana = **3 a 4 horas** semanales." En realidad, 15-20 min × 4 = 60-80 min, es decir **1 a 1,3 horas**.

Para llegar a 3-4 horas harían falta unas 12 sesiones semanales. Corregir el resultado, o explicar el supuesto (por ejemplo, número de sesiones por asignatura).

### 3.3 🟠 Tabla 11: título duplicado

La Tabla 11 tiene el mismo título que la Tabla 10 ("Resumen de componentes…"), también en la Lista de tablas. Título sugerido: **"Tabla 11. Tiempos promedio de ejecución por componente y tiempo total de marcaje"**.

Para el `(PENDIENTE)%` de 9.2 usar: **reducción = (T_manual − 3,2) / T_manual × 100**. Por ejemplo, si el tiempo manual medido fuera 17,5 min, la reducción sería 81,7%.

---

## 4. Citas frente a las fuentes del cuaderno

Se abrieron los PDF y las páginas cargadas en NotebookLM. Estos son los problemas encontrados.

### 4.1 🔴 El 35,4% está atribuido a dos autores distintos

- En la Introducción y en 5.1.1, el 35,4% es de **Mejía y Ordóñez (2004)**. Esto es correcto: la Tabla 1 del PDF dice "Firmar lista por compañero … 35,4".
- En el Estado del arte local (4.3) se le atribuye a **Martínez y Ramírez (2018)**. Esto es incorrecto: ese artículo no reporta el 35,4%.
- El dato es solo de la **Universidad de los Andes** (2004), no de "universidades del país", como dice el Capítulo 7.

**Pegar en 4.3**, en lugar de la frase del 35,4%:
> Los hallazgos revelan que más del 90% de los estudiantes encuestados admitió haber cometido algún tipo de fraude durante su vida universitaria, sin cambios significativos entre 2003 y 2013, y que dejar copiar en un examen, incluir a alguien en un grupo sin haber trabajado y prestar un trabajo son las conductas más frecuentes.

**En el Capítulo 7, cambiar** "35.4% de firmas por terceros en universidades del país" por "35,4% de firmas por terceros en la Universidad de los Andes".

### 4.2 🔴 El 89% no es de asistencia, no es de aulas y no lo midió Ríos-Avendaño

En el artículo, Ríos-Avendaño et al. (2024) **citan** una encuesta del programa *Antioquia Legal* (García, 2013): más de 5.900 estudiantes de 15 instituciones, donde "el 89% indica que ha suplantado a un compañero **en un examen**". Es un dato de 2012-2015, **anterior a la pandemia**, y se refiere a exámenes, no a la asistencia.

El texto actual lo presenta como suplantación "en las aulas" y lo mezcla con la pandemia (Planteamiento, Introducción, 5.1.1 y Capítulo 7).

**Pegar en el Planteamiento del problema**, en lugar de la frase del 89%:
> En Antioquia, la encuesta del programa Antioquia Legal, aplicada a más de 5.900 estudiantes de 15 instituciones de educación superior, encontró que el 89% había suplantado a un compañero en un examen (García, 2013, citado en Ríos-Avendaño et al., 2024). Con la educación remota durante la pandemia aparecieron nuevas modalidades, como conectarse en nombre de otro estudiante y simular la asistencia virtual a una actividad académica (Ríos-Avendaño et al., 2024).

Hacer el mismo ajuste en la Introducción, 5.1.1 y el Capítulo 7.

### 4.3 🟠 Martínez y Ramírez (2018): matices que faltan

- Las encuestas son de **2003 a 2013**, no "datos históricos" sin fecha.
- Los propios autores advierten que **los datos no son generalizables** a todas las universidades del país. Hoy el texto dice "más del 90% de los estudiantes universitarios" en general. Escribir "más del 90% de los estudiantes encuestados en cuatro universidades colombianas".
- "Estudios pioneros" no encaja con un artículo de 2018. Reservar "pionero" para Mejía y Ordóñez (2004).

### 4.4 🔴 Proctorizer como antecedente internacional

La fuente es una **entrada de blog comercial** (Proctorizer, 21 de marzo de 2023) que menciona de segunda mano un informe de la Universidad de Sídney: "el 12% admitió haber contratado a alguien para que hiciera sus **exámenes en línea**". El blog no describe ningún sistema, metodología ni resultados. No cumple lo que la plantilla FCBI pide para un antecedente ("¿Qué problema solucionó el autor? ¿Cómo lo hizo?").

Además, la tesis le añade cosas que el blog no dice: "o registre actividades académicas", "supervisión automatizada con IA, validación biométrica continua".

**Acción:** reemplazar este antecedente por **Nwabuwe et al. (2023)**, que ya está en el cuaderno y es casi el mismo sistema que el suyo: QR dinámico, geocerca e IMEI, con pruebas por escenarios de fraude. El dato de Proctorizer puede quedarse como contexto en el Planteamiento, citado como blog.

**Texto base para el nuevo antecedente internacional** (completar con el PDF):
> Nwabuwe, Sanghera, Alade y Olajide (2023), de la Nottingham Trent University (Reino Unido), desarrollan un sistema de monitoreo de asistencia que combina una aplicación móvil para escanear códigos QR, una aplicación web de página única que genera el código y administra los dispositivos, una geocerca alrededor del aula y la verificación del IMEI del teléfono, más un algoritmo que cambia el código QR a intervalos definidos. [Completar: metodología de pruebas y resultados por escenario, desde la sección de evaluación del PDF.]
>
> Este trabajo aporta al proyecto la arquitectura de validación por capas (QR dinámico, geocerca y verificación del dispositivo), que se adoptó y amplió con la verificación facial. A diferencia de ese sistema, en este proyecto el IMEI se reemplazó por una huella SHA-256 del dispositivo debido a las restricciones de privacidad de Android e iOS.

### 4.5 🔴 Referencias con autores o revistas que no coinciden con la fuente real

| En la bibliografía actual | Fuente real (según el PDF del cuaderno) |
|---|---|
| Cano-Perfecto, A., Martínez-Mendoza, R., & García-López, M. (2026). … *Revista IPSUMTEC*, 7(2), 19-28 | Cano Perfecto, J. E., Ramírez Ruiz, S. Y., Gallegos Olvera, P. A., Varela Leija, N. G., & Hernández-Sierra, M. G. (2026). *Ciencia Latina Revista Científica Multidisciplinar*, 10(1). Los coautores y la revista son otros |
| Nwabuwe, C., & Adewale, O. (2023). *Journal of Academic Technology and Cybersecurity*, 4(1), 104-118 | Nwabuwe, A., Sanghera, B., Alade, T., & Olajide, F. (2023). *International Journal of Advanced Computer Science and Applications (IJACSA)*, 14(4). Cuatro autores, por eso "et al." |
| Mejía, J. F., & Ordóñez, O. L. (2004). *Revista Educación y Pedagogía*, 16(39), 87-99 | Mejía, J. F., & Ordóñez, C. L. (2004). *Revista de Estudios Sociales*, (18), 13-25 |
| Martínez, J., & Ramírez, L. (2018). *Revista de Educación Superior y Desarrollo*, 12(1), 45-62 | Martínez, L., & Ramírez, R. E. (2018). *Educação e Pesquisa*, 44, e157079 |
| Ríos-Avendaño, A., Gómez-Gómez, M., & Pérez-Vásquez, D. (2024). *Revista de Gestión Educativa y Calidad*, 15(2), 112-130 | Ríos-Avendaño, C., Ocampo-Salazar, C., & Núñez, M.-A. (2024). *Revista Iberoamericana de Educación Superior*, 15(42) |
| Hurtado-Pardo, C., & Llanos-Bermúdez, D. (2021). Repositorio … **Universidad Santo Tomás** | Hurtado Pardo, E. F., & Llanos Bermúdez, J. E. (2021). Repositorio **Universidad Distrital Francisco José de Caldas**. El texto de 4.2 sí dice Distrital; la bibliografía no |
| SIC (2025). Doctrina … Radicado No. 180171259 | El radicado **18-171259-1 es un concepto de 2018**. Lo de 2025 es la **Resolución 52185 de 2025** (28 de agosto) sobre el conjunto residencial. Son dos referencias distintas |
| MinTIC (2013). Decreto 1377 | Lo expide el **Presidente de la República** (firman MinCIT y MinTIC). *Diario Oficial* **48.834** |
| Ley 1581 de 2012, 17 de octubre, *Diario Oficial* 48.583 | *Diario Oficial* **48.587** del **18 de octubre** de 2012 |

**Citadas en el texto pero ausentes de la bibliografía** (hay que añadirlas):
- **Canico et al. (2024)**, citada 5 veces. Es el PDF IPSUMTEC del cuaderno.
- **Chin et al. (2015)**.
- **Regula (2026)**. La página del cuaderno es del 27 de octubre de 2025.
- **García (2013)**, si se adopta la redacción de 4.2.

**En la bibliografía pero nunca citada:** Sentencia C-748 de 2011. Citarla en el Marco legal (es la que declara exequible la Ley 1581) o quitarla.

**Cita que no sostiene lo que se afirma:** en el glosario, la definición de BYOD cita a Chin et al. (2015). Ese artículo trata la motivación con materiales de *u-learning* por QR, no BYOD. Buscar otra fuente para esa definición o quitar la cita.

### 4.6 🟡 Ley 2502 de 2025: precisar el agravante

La ley aumenta **la multa** hasta en una tercera parte cuando la falsedad personal se comete con IA. El texto dice "agravante punitivo de hasta una tercera parte" sin decir sobre qué. Escribir "aumenta la multa hasta en una tercera parte".

---

## 5. Huecos de información (qué recolectar y dónde ponerlo)

### 5.1 🔴 Objetivo 1: datos de campo que faltan

| Marcador | Dato que hay que conseguir | Cómo |
|---|---|---|
| P0460 `(PENDIENTE)` estudiantes | N.º de estudiantes que respondieron la encuesta | Exportar las respuestas del formulario |
| P0460 `(PENDIENTE)` docentes | N.º de docentes entrevistados (en 9.1 son 3) | Lista de entrevistas |
| P0461 `(PENDIENTE)` sesiones | N.º de sesiones cronometradas | Hoja de cronometraje |
| **Tabla 2 completa** | Minutos promedio de cada actividad, % del tiempo de clase y fallas observadas | Cronometraje. % = minutos / 120 × 100 |
| P0464 dos `(PENDIENTE)` | Minutos totales por sesión y % de tiempo perdido | Total de la Tabla 2 |
| **Figura 2** (no tiene gráfica) | Gráfico de barras con el % de cada conducta admitida | Respuestas de la encuesta |
| P0490 `(PENDIENTE)%` | % de estudiantes que firmaron por otro; % de docentes que vieron QR o enlaces reenviados | Encuesta y entrevistas |
| P0491 `(PENDIENTE)%` | % de docentes insatisfechos | Entrevistas |
| 9.2 `(PENDIENTE)` | % de reducción y minutos del método manual | Fórmula de 3.3 |

Muestra: 5.3.3 y 9.1 dicen **64 estudiantes en 4 grupos**. Si la encuesta tiene otro número, explicar la diferencia.

Poner los instrumentos (encuesta, guion de entrevista, formato de cronometraje) en **Anexos A, B y C**. La plantilla exige la sección Anexos y hoy no existe.

### 5.2 🔴 Usabilidad: prometida y no reportada

La usabilidad aparece en el Resumen ("percepción favorable de usabilidad"), en el Objetivo 3, en 6.2, en la Tabla 1 ("cuestionarios de usabilidad") y en la Introducción, pero **el Capítulo 9 no presenta ningún resultado de usabilidad**. Un jurado verificará este objetivo.

**Acción:** añadir una sección **9.5 Evaluación de usabilidad**. Opción recomendada: el cuestionario **SUS (System Usability Scale)**, de 10 preguntas con puntaje de 0 a 100, aplicado a estudiantes y a los 3 docentes. Incluir el puntaje promedio, la desviación estándar y su interpretación (68 o más se considera por encima del promedio). Poner el cuestionario en un anexo.

### 5.3 🟠 Otros datos que el Capítulo 9 promete y no muestra

- **Precisión de la geocerca en metros** (prometida en 6.2, Tabla 1 y 9.1). Reportar el error GPS promedio dentro del aula y cuántos estudiantes **legítimos** fueron rechazados por la geocerca.
- **Falsos rechazos biométricos.** Solo se midieron ataques bloqueados. Falta cuántas veces un estudiante **real** fue rechazado (coseno < 0,75 siendo él mismo). Sin este dato, el umbral de 0,75 no está justificado.
- **Adopción de la ruta alternativa** (9.1 y Tabla 1: "nivel de aceptación"). Indicar cuántos de los 64 estudiantes eligieron la ruta no biométrica y por qué.
- **Resultado del consentimiento.** Indicar cuántos aceptaron el aviso de privacidad.

### 5.4 🟠 Justificación: el capítulo empieza sin texto propio

Después del título "JUSTIFICACIÓN" el documento pasa directo a "ALCANCE". Falta un párrafo que justifique el proyecto: por qué es conveniente, para quién y qué aporta a Unicatólica y a la Ingeniería de Sistemas. Hay material en las cifras del Planteamiento y en las secciones de impacto.

### 5.5 🟠 Marco legal incompleto

La sección dice analizar "pronunciamientos jurisprudenciales", pero no incluye ninguno. Faltan normas que sí están en el cuaderno:

| Norma | Por qué incluirla | Dónde usarla |
|---|---|---|
| **Constitución, Art. 15** | Fundamento del Habeas Data (ya está en la bibliografía) | Abrir el Marco legal |
| **Decreto 1377 de 2013, Art. 6** | Dice literalmente "Ninguna actividad podrá condicionarse a que el Titular suministre datos personales sensibles". Es la base de la ruta alternativa | Justifica 8.9 y la Tabla 13 |
| **Concepto SIC 18-171259 (2018)** | Para datos biométricos hace falta autorización escrita y no se puede restringir una actividad a su entrega | Igual |
| **Resolución SIC 52185 de 2025** | La SIC ordenó a un conjunto residencial habilitar mecanismos alternativos no invasivos y borrar datos biométricos de reconocimiento facial. Es un caso real y reciente | Ejemplo en Limitaciones y en la Tabla 13 |
| **Sentencia C-748 de 2011** | Control de constitucionalidad de la Ley 1581 | Ya está en la bibliografía |
| **Ley 1581, Art. 23** | Multas de hasta 2.000 SMMLV | Citarla en 2.5 (Impacto económico), donde hoy aparece la cifra sin artículo |

### 5.6 🟠 Tabla 13: incompleta y autoevaluada

- La Ley 1581 (Art. 4) tiene **8 principios**: legalidad, finalidad, libertad, veracidad o calidad, transparencia, acceso y circulación restringida, seguridad y confidencialidad. La tabla menciona 4, y "Voluntariedad y no condicionamiento" no es uno de ellos (viene del Art. 6 y del Decreto 1377). Completar los 8, o explicar por qué solo aplican esos.
- Fila **Seguridad**: dice que "no se almacenan imágenes", pero **la plantilla facial de 192 dimensiones sí es un dato biométrico sensible y sí se guarda** en `student_biometrics`. Indicar cómo se protege (cifrado en reposo, acceso por rol), cuánto tiempo se conserva y cómo se borra (en la Tabla 6 el estudiante puede eliminarla; decirlo aquí).
- "Cumplido al 100%" en las cuatro filas es una autoevaluación. Cambiar la columna a "Mecanismo implementado" o "Implementado". El cumplimiento legal lo certifica la institución, no el prototipo.
- Falta mencionar quién es el **responsable del tratamiento** (Unicatólica) y la **política de tratamiento** (Decreto 1377).

### 5.7 🟡 Marcadores de plantilla sin llenar

- P0021: "Título de tu director de trabajo de grado". Poner el título académico del profesor Peñaranda (por ejemplo, "Ingeniero de Sistemas, Mg. en …").
- P0053: "Santiago de Cali, día del mes de año".
- La tabla de contenido, las listas de figuras y las listas de tablas tienen números de página escritos a mano. La plantilla pide generarlos automáticamente: Referencias → Actualizar tabla.

---

## 6. Estructura frente a la plantilla FCBI

| Plantilla FCBI | Documento actual | Acción |
|---|---|---|
| 1. Planteamiento → 1.1 Formulación, 1.2 Sistematización | Subtítulos sin número | Numerar 1.1 y 1.2 |
| 2. Justificación → subsecciones | Alcance, Limitaciones e Impacto social sin número; Ambiental y Económico como 2.4 y 2.5 | Numerar 2.1-2.5 y añadir el párrafo de justificación (5.4) |
| 4. Marco referencial (4.1 teórico, 4.2 conceptual, 4.3 contextual, 4.4 legal) | Se agregó "4. Estado del arte" como capítulo y el Marco pasó a ser el 5 | La plantilla dice "no debes crear más capítulos de los ya establecidos". **Consultar con el director**: o se integra el Estado del arte dentro del Marco referencial, o se deja con su aprobación |
| 5.4 Tratamiento de la información (5.4.1 Técnicas estadísticas, 5.4.2 Presentación) | No existe | Añadir: estadística descriptiva (media, %), SUS y tablas/figuras |
| 6, 7, 8 Desarrollo de objetivos | 7, 8, 9 (por el capítulo extra) | Se corrige solo si se resuelve lo anterior |
| 9. Conclusiones / 10. Recomendaciones | Sin número y vacíos | Numerar |
| Bibliografía (sin número) | "4. BIBLIOGRAFÍA" | Quitar el "4." |
| Anexos | No existe | Crear los Anexos A, B, C… |
| 5.2.6 | Escrito como texto normal, no como Título 3, por eso no aparece en el índice | Aplicar el estilo Título 3 |

Otros puntos de formato:
- La plantilla pide **APA 7.ª edición**.
- **Resumen**: debe tener entre 100 y 300 palabras y estructura OMRC. Hoy tiene unas 270 palabras, pero sus resultados son vagos ("alta precisión", "percepción favorable"). Cuando tengan los datos, poner cifras: minutos medidos, 99,3%, puntaje SUS.
- **Estado del arte**: la guía del Seminario (clase 6) pide que al menos el 70% de las referencias empíricas sean de los últimos 5 a 10 años. Mejía y Ordóñez (2004) sirve como antecedente histórico, no como estado del arte.
- **Separador decimal**: en español/ICONTEC es la coma (35,4%). El documento usa el punto (35.4%). Unificar.

### Erratas puntuales

| Ubicación | Dice | Debe decir |
|---|---|---|
| Sistematización, pregunta 3 | Ley **15811** de 2012 | Ley 1581 de 2012 |
| Título de 9.4 | LEY **1582** DE 2012 | LEY 1581 DE 2012 |
| Dedicatoria | "Dedicatória" | "Dedicatoria" |
| Dedicatoria | "alcanzar **esté** logro" | "este logro" |
| Agradecimientos | "**A el** profesor" | "Al profesor" |
| Tabla 8 y Tabla 9 | "La API **válida**" / "**válida** hash" | "valida" |
| Sistematización, pregunta 3 | "escaneo biométrico facial **multiangular**" | No aparece en ninguna otra parte. Quitar "multiangular" |
| Planteamiento | "Martinez y Ramirez", "Mejia y Ordoñez", "Rios-Avendaño" | Con tildes, como en el resto del documento |
| Planteamiento | "clase virtuales" | "clases virtuales" |
| 5.2.4 | "GEOCERCA **y** GEOLOCALIZACIÓN" | "GEOCERCA Y GEOLOCALIZACIÓN" |
| 5.2.5 | "VERIFICACION" | "VERIFICACIÓN" |
| 5.1.3 | "PROTECCIÓN DE DATOS SENSIBLE" | "SENSIBLES" |

---

## 7. Revisión de estilo con humanizalo

**Adaptación:** humanizalo está pensada para textos generales. Algunas de sus reglas (escribir en primera persona, opinar, usar humor) **chocan con la plantilla FCBI**, que exige tercera persona, voz activa, pasado y tono objetivo. Se aplicaron solo los patrones compatibles con la redacción académica: inflación de importancia, vocabulario típico de IA, conectores repetidos, afirmaciones absolutas, relleno y tríadas forzadas.

### 7.1 Patrones encontrados (conteo en el cuerpo del texto)

| Patrón (ID) | Expresiones en el documento | Veces | Qué hacer |
|---|---|---|---|
| P09 Vocabulario de IA | "garantizar/garantiza" | 19 | Reservar "garantizar" para lo que de verdad se garantiza; en lo demás, "asegura", "busca" o el verbo concreto |
| P09 | "permite/permitió" | 25 | Escribir directamente qué hace el sistema |
| P09 | "optimizar" | 14 | "reducir el tiempo", "acelerar" |
| P09 | "en tiempo real" | 13 | Usarlo solo donde aplique (el panel consulta cada 5 s; eso no es tiempo real estricto) |
| P01 Inflación de importancia | "fundamental", "indispensable", "crítico", "contundente", "robusto", "pilar", "eje estratégico" | ≈18 | Quitar el adjetivo o reemplazarlo por el dato |
| P13 Extremos | "elimina", "erradica", "100%", "estricto cumplimiento", "estrictamente" | ≈36 | Es el patrón más riesgoso: un jurado cuestionará cualquier "elimina" o "100%". Usar cifras medidas |
| P39 Relleno | "de manera/de forma + adjetivo" | 22 | "de forma manual" → "manualmente", o reestructurar la frase |
| P24/P26 Conectores repetidos | "Asimismo" (14), "En este/el contexto" (9), "Finalmente" (6) | 29 | Variar o eliminar; muchos párrafos funcionan sin conector |
| P22 Paralelismo negativo | "no solo… sino que también…", "va más allá de… sino" | 4 | Decir directamente las dos cosas |
| P23 Tríadas forzadas | "eficiencia operativa y la toma de decisiones…", "disciplina y responsabilidad", "intimidad y la autodeterminación…" | varias | Dejar uno o dos elementos con contenido real |
| P11 Adverbios en -mente | "directamente", "predominantemente", "gravemente", "explícitamente"… | 70 | Quitar al menos la mitad |
| P08 Declaraciones vagas | "genera una mala calidad en el entorno educativo y social", "efectividad general altamente satisfactoria" | varias | Reemplazar por el hecho concreto |
| P27 Raya (—) | Tabla 5 | 2 | Aceptable en tablas; no usarla en el texto corrido |

### 7.2 Ejemplos de reescritura

Son ejemplos para que vean el criterio; el texto final lo deben escribir ustedes.

**Introducción, primer párrafo**

Antes:
> Actualmente, la transformación digital en las Instituciones de Educación Superior se ha consolidado como un eje estratégico para la optimización de los procesos de gestión académica y administrativa, convirtiendo la automatización de la información en un pilar indispensable para la eficiencia operativa y la toma de decisiones.

Después:
> Las instituciones de educación superior han digitalizado buena parte de su gestión académica, pero el registro de asistencia en el aula sigue haciéndose, en muchos casos, con listas de papel o llamado a viva voz.

**Cierre de 9.4**

Antes:
> …no solo es técnicamente viable y altamente eficiente […] sino que logra eliminar la suplantación de identidad con un 99.4% de efectividad.

Después:
> En las pruebas de campo, el grupo completo registró su asistencia en 3,2 minutos en promedio, y el sistema bloqueó 144 de los 145 intentos de fraude simulados (99,3%).

**Cierre del Capítulo 8**

Antes:
> …dejando la plataforma 100% lista para la fase de pruebas piloto…

Después:
> Con los siete componentes integrados, el prototipo pasó a la fase de pruebas piloto del tercer objetivo.

### 7.3 Puntaje humanizalo del texto actual (orientativo)

| Dimensión | Puntaje | Motivo |
|---|---|---|
| Directness | 5/10 | Mucho andamiaje ("En este contexto", "Esta elección se justifica por…") |
| Rhythm | 4/10 | Párrafos largos con la misma estructura; frases de 50 a 70 palabras |
| Trust | 5/10 | Repite las mismas cifras en 4 secciones (Introducción, Planteamiento, 5.1.1 y Capítulo 7) |
| Authenticity | 4/10 | Vocabulario de IA y absolutos ("elimina", "100%") |
| Density | 5/10 | Mucho relleno, aunque hay contenido técnico real |
| Soul | 6/10 | El Capítulo 8 tiene decisiones técnicas propias (sin ORM, sin IMEI, ventana de 3 s); eso es lo mejor del documento |
| **Total** | **29/60** | El umbral de la skill es 42/60. Corregir P13, P09 y los conectores debería subirlo por encima de 40 |

**Redundancia:** las estadísticas de fraude (más del 90%, 35,4% y 89%) aparecen casi idénticas en la Introducción, el Planteamiento, 5.1.1 y el Capítulo 7. Dejarlas completas en el Planteamiento; en la Introducción, una frase; en 5.1.1, solo la teoría y una remisión al Planteamiento; en el Capítulo 7, solo como comparación con sus propios datos.

---

## 8. Bibliografía corregida (APA 7) para pegar

Ordenar alfabéticamente al pegar. Lo que aparece entre [corchetes] se completa con el PDF.

```
Cano Perfecto, J. E., Ramírez Ruiz, S. Y., Gallegos Olvera, P. A., Varela Leija, N. G., & Hernández-Sierra, M. G. (2026). Sistema de toma de asistencia estudiantil con código QR, biometría y geolocalización en tiempo real. Ciencia Latina Revista Científica Multidisciplinar, 10(1), [páginas]. https://doi.org/10.37811/cl_rcm.v10i1.22615

Canico Hernández, A., Medina de la Rosa, P., & Cortés Sánchez, O. (2024). Sistema de pase de lista por medio de código QR. IPSUMTEC, 7(2), 174-[página final]. https://doi.org/10.61117/ipsumtec.v7i2.323

Chin, K.-Y., Lee, K.-F., & Chen, Y.-L. (2015). Impact on student motivation by using a QR-based U-learning material production system to create authentic learning experiences. IEEE Transactions on Learning Technologies, [volumen(número)], [páginas].

Congreso de la República de Colombia. (2012, 17 de octubre). Ley Estatutaria 1581 de 2012: Por la cual se dictan disposiciones generales para la protección de datos personales. Diario Oficial No. 48.587.

Hurtado Pardo, E. F., & Llanos Bermúdez, J. E. (2021). Sistema de control de asistencia a estudiantes mediante carnet virtual con código QR [Trabajo de grado, Universidad Distrital Francisco José de Caldas]. Repositorio Institucional UD. https://repository.udistrital.edu.co/items/f2aa0251-70a5-4c09-808f-e3dd2934ee4c

Martínez, L., & Ramírez, R. E. (2018). Fraude académico en universitarios en Colombia: ¿Qué tan crónica es la enfermedad? Educação e Pesquisa, 44, e157079. https://doi.org/10.1590/S1517-9702201706157079

Mejía, J. F., & Ordóñez, C. L. (2004). El fraude académico en la Universidad de los Andes: ¿Qué, qué tanto y por qué? Revista de Estudios Sociales, (18), 13-25.

Montañez-Díaz, B. A., García-Gutiérrez, W. F., Prieto-Pastor, R. A., & Mendoza-De-los-Santos, A. (2024). Aplicación móvil para el control de asistencia de docentes universitarios con autenticación biométrica y verificación de geolocalización. Revista Científica de Sistemas e Informática, 4(2), e647. https://doi.org/10.51252/rcsi.v4i2.647

Nwabuwe, A., Sanghera, B., Alade, T., & Olajide, F. (2023). Fraud mitigation in attendance monitoring systems using dynamic QR code, geofencing and IMEI technologies. International Journal of Advanced Computer Science and Applications, 14(4), [páginas]. [DOI: verificar en el PDF]

Presidencia de la República de Colombia. (2013, 27 de junio). Decreto 1377 de 2013: Por el cual se reglamenta parcialmente la Ley 1581 de 2012. Diario Oficial No. 48.834.

Proctorizer. (2023, 21 de marzo). Mercado negro de suplantación de identidad en exámenes online, ¿cómo funciona y cómo protegerse de él? [Entrada de blog]. https://proctorizer.com/blog/

Regula. (2025, 27 de octubre). Verificación de identidad digital para la educación: Situación actual. Regula Forensics. [URL]

Ríos-Avendaño, C., Ocampo-Salazar, C., & Núñez, M.-A. (2024). Gestión del riesgo de fraude académico en educación superior. Un análisis en universidades de Medellín, Colombia, en tiempos de COVID-19. Revista Iberoamericana de Educación Superior, 15(42), [páginas]. https://doi.org/10.22201/iisue.20072872e.2024.42.1670

Superintendencia de Industria y Comercio. (2018). Concepto sobre tratamiento de datos sensibles biométricos (Radicación 18-171259-1).

Superintendencia de Industria y Comercio. (2025, 28 de agosto). Resolución 52185 de 2025: Orden de habilitar mecanismos de ingreso que no impliquen el tratamiento de datos biométricos. [URL de la sede electrónica]
```

Revisar en la fuente la entrada "SIC (2018). Guía para la gestión de riesgos…". En el cuaderno no hay una guía con ese título. Si el glosario la usa para definir biometría facial, cambiar esa cita por el concepto 18-171259.

---

## 9. Fuentes del cuaderno que no se aprovechan

Pueden fortalecer el Estado del arte y el Marco teórico:

| Fuente del cuaderno | Uso sugerido |
|---|---|
| **Montañez-Díaz et al. (2024)**, Universidad Nacional de Trujillo: app móvil con biometría y geolocalización | Antecedente internacional técnico (más cercano a su solución que Proctorizer) |
| **Nwabuwe et al. (2023)**, IJACSA: QR dinámico, geocerca e IMEI | Antecedente internacional (ver 4.4) |
| **Canico et al. (2024)**, IPSUMTEC | Ya se cita; falta en la bibliografía |
| "Biometría dactilar: una nueva alternativa…" | Antecedente de comparación de biometría (verificar el país del estudio) |
| "Implementación de un sistema de control de asistencia con código QR – Ricardo Palma, Carhuaz (2019)" | Antecedente QR estático, para contrastar con el QR dinámico |
| "Sistema informático para el control de asistencia en ambiente web" | Antecedente web |
| Noticia RCN: red de suplantación en la Universidad del Magdalena (al menos 30 jóvenes) | Segundo caso nacional en el Planteamiento, además de la UdeA |
| "Vida universitaria… fraude académico" (Revista Universidad de La Salle) | Marco teórico del fraude (fraude activo y pasivo) |
| "El fraude académico en los procesos de evaluación…" (UAH) | Marco teórico |
| MetaRed, "Campus seguros e inteligentes" | Justificación (transformación digital universitaria) |

El **Estado del arte local** (4.3) no tiene ningún antecedente **tecnológico** de Cali o del Valle. Martínez y Ramírez (2018) es un estudio de fraude, no de un sistema. Si no encuentran uno local, explicar esa ausencia: es un vacío de investigación que justifica el proyecto.

---

## 10. Qué falta para terminar el proyecto (lista de trabajo)

En orden recomendado:

1. **Recolectar los datos del Objetivo 1** (sección 5.1) y llenar los `(PENDIENTE)`, la Tabla 2 y la Figura 2.
2. **Aplicar el SUS** y escribir la sección 9.5 de usabilidad (5.2).
3. Medir los **falsos rechazos** (biometría y geocerca) y la **adopción de la ruta alternativa** (5.3).
4. Corregir las **incoherencias técnicas** de la sección 2: Redis/Docker, IMEI, tiempo de rotación del QR, FaceAPI y 3 o 4 objetivos.
5. Corregir los **cálculos** de la sección 3.
6. Corregir las **citas mal atribuidas** (4.1-4.4) y **reemplazar la bibliografía** (sección 8).
7. Completar el **Marco legal** (5.5) y la **Tabla 13** (5.6).
8. Escribir el **párrafo de Justificación** (5.4).
9. Ajustar la **numeración** a la plantilla y consultar con el director lo del Estado del arte (sección 6).
10. Hacer la **pasada de estilo** (sección 7).
11. Redactar **Conclusiones y Recomendaciones** (guía abajo; no se redactan aquí).
12. Actualizar el **Resumen y el Abstract** con los números finales. Deben escribirse **después** de las conclusiones, porque hoy el resumen afirma resultados que aún no existen.
13. Crear los **Anexos** y regenerar los índices automáticos.

### Guía para Conclusiones (no redactadas)

Según la plantilla FCBI: **mínimo 3 conclusiones por objetivo específico**, en **pasado**, una por párrafo, cada una ligada a un resultado concreto del capítulo. Con 3 objetivos son 9 o más párrafos.

| Objetivo | Resultados en los que debe apoyarse cada conclusión |
|---|---|
| 1. Diagnóstico | (a) minutos y % de tiempo perdido medidos (Tabla 2); (b) % de firmas por terceros y comparación con el 35,4% de Mejía y Ordóñez; (c) reenvío de QR estáticos o enlaces reportado por los docentes, que justificó el QR dinámico |
| 2. Diseño e implementación | (a) decisión de prescindir de Redis y del ORM, y su efecto; (b) reemplazo del IMEI por la huella SHA-256 por restricciones de privacidad; (c) biometría en el dispositivo sin enviar fotos (vector 192-D) y separación de las rutas biométrica y alternativa |
| 3. Validación | (a) tiempo de grupo de 3,2 min frente al manual y % de reducción; (b) 144 de 145 ataques bloqueados, con la debilidad de la foto o pantalla (1 de 15 pasó); (c) puntaje SUS; (d) adopción de la ruta alternativa y cumplimiento del Art. 6 del Decreto 1377 |

Evitar en las conclusiones: "elimina", "100%", "garantiza totalmente" y repetir el resumen.

### Guía para Recomendaciones (no redactadas)

La plantilla pide recomendaciones dirigidas **a la empresa (Unicatólica), a la universidad o a quien quiera continuar el proyecto**, claras y precisas. Temas que salen de las limitaciones encontradas en esta revisión:

- **Para Unicatólica:** política de tratamiento de datos biométricos y responsable designado; integración con Banner; piloto en más programas y en otro periodo; definir en el reglamento el umbral de faltas para las alertas.
- **Técnicas, para quien continúe:** prueba de vida pasiva o detección de *deepfakes* (relacionado con la Ley 2502 y con el ataque que pasó en la Tabla 12); cifrado en reposo de las plantillas; reemplazar el *polling* de 5 s por WebSockets; calibrar el umbral de coseno con una medición de falsos rechazos y aceptaciones; validar la geocerca en aulas de varios pisos (el error GPS en interiores es alto).
- **Investigativas:** medir el efecto en la tasa de deserción real a lo largo de un semestre completo.
