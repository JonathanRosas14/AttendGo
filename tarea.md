# Textos para pegar en el Trabajo de grado

Acompaña a `Revision coherencia - Trabajo de grado.md`. Cada bloque dice **dónde** va y **qué reemplaza**.

- `[DATO: …]` = un número que todavía tienen que medir. No lo inventen.
- `[VERIFICAR: …]` = algo que deben confirmar en el PDF o con el director.
- Los textos que describen el sistema se basaron en el código de `AttendGoMVP/backend` y `AttendGoApp`.

> ⚠️ **Tres diferencias entre la tesis y el código** que cambian varios textos de abajo:
> 1. **El QR no lleva un token cifrado.** Es un **código numérico de 6 dígitos** que el servidor genera y renueva cada **5 segundos** (configurable de 5 a 300 s), con 3 s de tolerancia para el código anterior. Corrijan "tokens cifrados" y "verificar firma de QR" en todo el documento.
> 2. **La alerta de riesgo no usa un porcentaje de faltas**, sino una **racha de 4 inasistencias consecutivas** (`AT_RISK_ABSENCE_STREAK = 4`).
> 3. **Hoy no existe ruta alternativa cuando el docente exige biometría.** Si la sesión tiene `biometric_required = true` y el estudiante no envía el reto facial, el servidor responde 428 y no deja marcar. La única salida es el **registro manual del docente**. Hay dos opciones: (a) cambiar el código para que el estudiante sin autorización biométrica pase por QR + GPS + huella, o (b) describir en la tesis que la ruta alternativa es el registro manual del docente. Abajo están los textos para la opción (b), que es la que corresponde al código actual. Si eligen (a), avísenme y ajusto los textos.

---

## A. Portada y preliminares

**P0021**, reemplazar "Título de tu director de trabajo de grado":
```
[VERIFICAR: título académico del profesor, ej. Ingeniero de Sistemas, Magíster en …]
```

**P0053**:
```
Santiago de Cali, [día] de [mes] de 2026
```

**Erratas:**
- "Dedicatória" → "Dedicatoria"
- "alcanzar esté logro" → "alcanzar este logro"
- "A el profesor Gabriel Peñaranda Rubio director de este trabajo de grado, que, con su conocimiento" → "Al profesor Gabriel Peñaranda Rubio, director de este trabajo de grado, quien con su conocimiento"

**Lista de tablas**, título de la Tabla 11:
```
Tabla 11. Tiempos promedio de ejecución por componente y tiempo total de marcaje
```

---

## B. Glosario

**AUTENTICACIÓN MULTIFACTOR (MFA)**, reemplazar completa:
```
AUTENTICACIÓN MULTIFACTOR (MFA): procedimiento de seguridad que exige verificar dos o más factores independientes, como algo que el usuario tiene, el lugar donde está o un rasgo físico, antes de conceder acceso o registrar una acción (Cano Perfecto et al., 2026).
```

**BIOMETRÍA FACIAL**, cambiar la cita "(Superintendencia de Industria y Comercio, 2018)" por:
```
(Cano Perfecto et al., 2026)
```

**CÓDIGO QR DINÁMICO**, reemplazar completa:
```
CÓDIGO QR DINÁMICO: código bidimensional cuyo contenido cambia a intervalos cortos, de modo que una imagen capturada o reenviada deja de ser válida en pocos segundos (Canico Hernández et al., 2024; Nwabuwe et al., 2023).
```

**MODELO BYOD**, quitar la cita de Chin et al. (2015), que no trata BYOD:
```
MODELO BYOD (BRING YOUR OWN DEVICE): esquema en el que estudiantes y docentes usan sus propios dispositivos móviles para ejecutar aplicaciones institucionales, sin que la institución deba adquirir equipos dedicados (Hurtado Pardo y Llanos Bermúdez, 2021).
```

**PRUEBA DE VIDA**, reemplazar completa:
```
PRUEBA DE VIDA (LIVENESS DETECTION): mecanismo que verifica que frente a la cámara hay una persona real y no una fotografía o un video. La prueba de vida activa pide al usuario realizar un gesto aleatorio, como parpadear o sonreír, dentro de un tiempo límite (Cano Perfecto et al., 2026; Regula, 2025).
```

**Nueva entrada**, en orden alfabético:
```
HUELLA DIGITAL DEL DISPOSITIVO (DEVICE FINGERPRINT): código generado con la función hash SHA-256 a partir de características del hardware, del sistema operativo y de un identificador de instalación del teléfono, que permite reconocer el mismo equipo en distintos registros sin almacenar datos que identifiquen directamente al usuario (Nwabuwe et al., 2023).
```

---

## C. Resumen y Abstract

Se reescriben **al final**, cuando estén todos los datos. Plantilla (100 a 300 palabras, estructura OMRC):

```
Se desarrolló un prototipo de plataforma web con aplicación móvil para el control de asistencia académica en la Fundación Universitaria Lumen Gentium (Unicatólica), con el fin de reducir el tiempo del pase de lista y la suplantación de estudiantes. Se realizó una investigación aplicada de desarrollo tecnológico, con enfoque mixto y diseño no experimental, en tres etapas. En el diagnóstico se encuestó a [DATO] estudiantes, se entrevistó a [DATO] docentes y se cronometraron [DATO] sesiones; el pase de lista manual tomó [DATO] minutos por sesión y el [DATO]% de los estudiantes admitió haber firmado por un compañero ausente. Luego se diseñó una arquitectura cliente-servidor en capas con PostgreSQL y se construyeron una aplicación web en Vue 3 y una aplicación móvil en React Native. El sistema combina un código QR que cambia cada cinco segundos, una geocerca por GPS, una huella del dispositivo y, cuando el docente la activa, la verificación facial con prueba de vida, procesada en el teléfono sin enviar fotografías. Para cumplir la Ley 1581 de 2012, el estudiante que no autoriza el uso de su rostro puede ser registrado por otra vía. En la prueba piloto con 64 estudiantes y 3 docentes, el grupo completo registró su asistencia en 3,2 minutos en promedio, el sistema bloqueó 144 de 145 intentos de fraude simulados (99,3%) y la usabilidad obtuvo [DATO] puntos en la escala SUS. Se concluyó que [completar con la conclusión principal, sin usar "elimina"].

Palabras clave: control de asistencia, código QR dinámico, biometría facial, geocerca, protección de datos personales.
```

En el Abstract, traducir este mismo texto.

---

## D. Introducción

**Párrafo 1**, reemplazar completo:
```
Las instituciones de educación superior han digitalizado buena parte de su gestión académica, pero en muchos casos el registro de asistencia en el aula sigue haciéndose con listas de papel o con el llamado a viva voz. La asistencia no es solo un trámite: permite seguir el desempeño de los estudiantes y detectar a tiempo el ausentismo. El registro manual consume tiempo de clase, se presta a errores de transcripción y facilita que un estudiante firme por otro.
```
(Quitar la cifra "15 y 20 minutos" de este párrafo, que no tiene cita.)

**Párrafo 2**, reemplazar desde "Investigaciones empíricas…" hasta "…(Ríos-Avendaño et al., 2024)." (la segunda vez) por:
```
En Colombia, Martínez y Ramírez (2018) encuestaron a más de 3.300 estudiantes de cuatro universidades entre 2003 y 2013, y encontraron que más del 90% admitió haber cometido algún tipo de fraude académico. En la Universidad de los Andes, el 35,4% de los estudiantes reconoció haber firmado una lista de asistencia a nombre de un compañero (Mejía y Ordóñez, 2004). Durante la educación remota por la pandemia aparecieron nuevas modalidades, como conectarse en nombre de otro estudiante o simular la asistencia a una actividad virtual (Ríos-Avendaño et al., 2024).
```
Dejar el caso de la Universidad de Antioquia como está.

**Párrafo 4**, cambiar:
- "el registro del identificador único de hardware para evitar…" → "una huella digital del dispositivo para detectar que un mismo teléfono se use para marcar a varias personas"
- "la verificación biométrica facial con algoritmos de prueba de vida en tiempo real" → "la verificación facial con una prueba de vida activa por gesto, procesada en el teléfono del estudiante"

**Párrafo 5 (metodología)**, reemplazar completo:
```
Para la ejecución del proyecto se adoptó una investigación aplicada de desarrollo tecnológico, con alcance descriptivo-proyectivo y enfoque mixto de carácter no experimental. El desarrollo del software siguió el marco ágil SCRUM y el modelado con UML. El trabajo se dividió en tres etapas, una por objetivo específico: el diagnóstico del registro manual en Unicatólica; el diseño y la construcción del prototipo, con una arquitectura cliente-servidor en capas, un backend en Node.js, Fastify, TypeScript y PostgreSQL desplegado con Docker, una aplicación web en Vue 3 y una aplicación móvil en React Native; y la validación técnica, de usabilidad y de cumplimiento de la Ley 1581 de 2012 mediante una prueba piloto en un entorno controlado.
```

**Párrafo 6 (organización del documento)**, reemplazar la numeración según cómo quede la estructura (ver sección M). Si el director acepta dejar el Estado del arte como capítulo:
```
El documento se organiza así: el Capítulo 1 presenta el planteamiento del problema; el Capítulo 2, la justificación, el alcance, las limitaciones y los impactos; el Capítulo 3, los objetivos; el Capítulo 4, el estado del arte; el Capítulo 5, el marco referencial; y el Capítulo 6, la metodología. Los Capítulos 7, 8 y 9 desarrollan cada objetivo específico, y los Capítulos 10 y 11 presentan las conclusiones y las recomendaciones.
```

---

## E. Planteamiento del problema

**Párrafo 1**, reemplazar completo:
```
El fraude académico es un problema persistente en las universidades colombianas. Martínez y Ramírez (2018) encontraron que más del 90% de los estudiantes encuestados en cuatro universidades del país admitió haber cometido algún tipo de fraude, sin cambios significativos entre 2003 y 2013. Una de esas conductas afecta directamente el registro de asistencia: en la Universidad de los Andes, el 35,4% de los estudiantes reconoció haber firmado una lista a nombre de un compañero (Mejía y Ordóñez, 2004). En Antioquia, la encuesta del programa Antioquia Legal, aplicada a más de 5.900 estudiantes de 15 instituciones, registró que el 89% había suplantado a un compañero en un examen (García, 2013, citado en Ríos-Avendaño et al., 2024). Con la educación remota durante la pandemia aparecieron modalidades como conectarse en nombre de otro estudiante y simular la asistencia virtual (Ríos-Avendaño et al., 2024). Frente a este panorama, las listas en papel y el llamado a viva voz facilitan la suplantación y consumen tiempo de clase (Canico Hernández et al., 2024).
```

**Párrafo 2**: corregir "Martinez y Ramirez", "Mejia y Ordoñez", "Rios-Avendaño" y "clase virtuales". La última frase, sobre la Ley 1581, reemplazarla por:
```
A esto se suma una restricción legal: la Ley 1581 de 2012 y el Decreto 1377 de 2013 clasifican los datos biométricos como sensibles y prohíben condicionar una actividad a su entrega, de modo que cualquier solución basada en el rostro debe ofrecer otra forma de registro (Superintendencia de Industria y Comercio, 2018).
```

**Párrafo 3**, primera frase:
```
Si estas vulnerabilidades persisten, los registros de asistencia dejan de reflejar la presencia real de los estudiantes.
```

**Sistematización, pregunta 3**, reemplazar:
```
¿De qué manera se puede validar la viabilidad técnica, la usabilidad y el cumplimiento de la Ley 1581 de 2012 del sistema propuesto, asegurando que el tratamiento de datos biométricos faciales no condicione el registro de asistencia del estudiante?
```

**Formulación del problema y sistematización**: numerar como 1.1 y 1.2.

---

## F. Justificación (Capítulo 2)

**Párrafo nuevo**, va justo debajo del título JUSTIFICACIÓN y antes de 2.1 ALCANCE:
```
El proyecto se justifica porque el registro manual de asistencia en Unicatólica no permite verificar quién está realmente en el aula y consume tiempo de clase. Para la institución, contar con registros confiables y centralizados permite detectar a tiempo a los estudiantes que acumulan inasistencias y respaldar los procesos de calidad académica. Para la Ingeniería de Sistemas, el proyecto aplica técnicas de verificación por capas, como el código QR dinámico, la geocerca, la huella del dispositivo y la biometría facial procesada en el teléfono, dentro de los límites que impone la legislación colombiana sobre datos sensibles. El uso de los teléfonos de los estudiantes evita que la universidad deba adquirir lectores biométricos para cada aula.
```

**Numeración**: 2.1 Alcance, 2.2 Limitaciones, 2.3 Impacto social, 2.4 Impacto ambiental, 2.5 Impacto económico.

**2.2 Limitaciones**, añadir al final:
```
La prueba de vida implementada es activa: pide al estudiante un gesto aleatorio, como parpadear o sonreír. No mide la profundidad del rostro ni se evaluó frente a videos o rostros generados con inteligencia artificial. Por otra parte, la huella del dispositivo es una señal antifraude y no un identificador infalible. En Android, el identificador de instalación se conserva aunque se reinstale la aplicación; en iOS cambia si el usuario desinstala todas las aplicaciones del mismo desarrollador. Además, un estudiante que use dos teléfonos distintos no es detectado por este control. Por último, la precisión del GPS dentro de edificios es variable, lo que puede producir rechazos de estudiantes que sí están en el aula.
```

**2.5 Impacto económico**, cambiar:
- "de un promedio de 15 a 20 minutos a menos de 5 minutos por clase" → "de [DATO] minutos a 3,2 minutos por clase, según la prueba piloto"
- "las cuales pueden alcanzar hasta los 2.000 salarios mínimos legales mensuales vigentes" → "las cuales pueden alcanzar hasta 2.000 salarios mínimos mensuales legales vigentes (Ley 1581 de 2012, Art. 23)"

---

## G. Objetivos

**Objetivo general**, cambiar el final "en las instituciones educativas del país" por:
```
en la Fundación Universitaria Lumen Gentium (Unicatólica).
```

**Objetivo específico 1**, cambiar "en las entidades educativas" por:
```
en el programa de Ingeniería de Sistemas de Unicatólica
```

---

## H. Estado del arte

### 4.1 Internacional: reemplazar el bloque de Proctorizer (dos párrafos) por:
```
Nwabuwe, Sanghera, Alade y Olajide (2023), de la Nottingham Trent University, en el Reino Unido, abordan la suplantación en los sistemas de asistencia basados en códigos QR, donde los estudiantes comparten el código para registrar a compañeros ausentes. Desarrollan un sistema compuesto por una aplicación móvil para escanear el código, una aplicación web que lo genera y administra los dispositivos, una geocerca alrededor del aula y una verificación del IMEI del teléfono, a lo que suman un algoritmo que cambia el código QR a intervalos definidos. [VERIFICAR en el PDF: metodología de pruebas y resultados por escenario de fraude.]

Este trabajo aporta al proyecto la validación por capas: código dinámico, geocerca y verificación del dispositivo. De él se adoptó la idea de combinar controles independientes para que un solo control evadido no permita el fraude. A diferencia de ese sistema, en este proyecto el IMEI se reemplazó por una huella SHA-256 del dispositivo, porque Android e iOS restringen el acceso al IMEI, y se añadió la verificación facial.
```

### 4.1 Cano Perfecto: cambiar "Cano-Perfecto et al." por "Cano Perfecto et al." y corregir el segundo párrafo:
```
Este trabajo aporta al proyecto la evidencia de que la verificación facial puede ejecutarse sin hardware dedicado. A diferencia de Cano Perfecto et al. (2026), que procesan el rostro en el navegador con FaceAPI.js, en este proyecto el rostro se procesa en el teléfono con TensorFlow Lite y solo se envía al servidor un vector numérico, sin fotografías. De su metodología se adoptó la estructura de pruebas alfa y beta en un entorno controlado.
```

### 4.2 Nacional: corregir solo los nombres
- "Hurtado-Pardo y Llanos-Bermúdez (2021)" → "Hurtado Pardo y Llanos Bermúdez (2021)"

### 4.3 Local: reemplazar la frase del 35,4%
Reemplazar "Los hallazgos revelan que el 35.4% de los estudiantes admite haber firmado listas de asistencia por otros y concluyen que…" por:
```
Los hallazgos revelan que más del 90% de los estudiantes encuestados admitió haber cometido algún tipo de fraude durante su vida universitaria, sin cambios significativos entre 2003 y 2013, y que dejar copiar en un examen, incluir a alguien en un grupo sin haber trabajado y prestar un trabajo son las conductas más frecuentes. Los autores advierten que sus datos no son generalizables a todas las universidades del país y concluyen que…
```

En el párrafo de aporte, cambiar "respaldado por el dato crítico del 35.4% de adulteración de firmas físicas" por:
```
respaldado por la persistencia del fraude a lo largo de una década
```

Cambiar también "recolectan datos históricos mediante encuestas" por "recolectan datos mediante encuestas aplicadas entre 2003 y 2013".

**Si no encuentran un antecedente tecnológico local**, añadir al final de 4.3:
```
En la revisión realizada no se encontraron sistemas de control de asistencia con verificación antifraude desarrollados o documentados en instituciones de educación superior de Cali. Esta ausencia constituye un vacío que el presente proyecto busca atender.
```

---

## I. Marco referencial

### 5.1.1, primer párrafo: reemplazar la repetición de cifras
Reemplazar desde "En el contexto colombiano, las investigaciones empíricas demuestran…" hasta el final del párrafo por:
```
En el contexto colombiano, los estudios citados en el planteamiento del problema muestran que el fraude académico es frecuente y estable en el tiempo (Martínez y Ramírez, 2018; Mejía y Ordóñez, 2004).
```

### 5.1.2, última frase:
```
Esta fundamentación orienta el segundo objetivo específico: el modelado de la arquitectura, la especificación de requerimientos y la construcción del prototipo.
```

### 5.1.3, reemplazar el título y los dos párrafos
Título: **5.1.3 AUTENTICACIÓN MULTIFACTOR Y PROTECCIÓN DE DATOS SENSIBLES**
```
La autenticación multifactor establece que la identidad se verifica con mayor confianza cuando se combinan factores independientes: algo que el usuario tiene, como un código QR vigente o su propio teléfono; el lugar donde se encuentra, verificado con una geocerca; y algo que el usuario es, como los rasgos del rostro (Nwabuwe et al., 2023). El código QR dinámico cambia cada pocos segundos, de modo que una captura reenviada por mensajería deja de servir. La geocerca compara la ubicación GPS del estudiante con la del aula, y la huella del dispositivo detecta que un mismo teléfono registre a varias personas.

En el componente biométrico, el reconocimiento facial compara los rasgos del rostro con una plantilla registrada previamente, y la prueba de vida activa pide un gesto aleatorio para descartar fotografías. Esta dimensión técnica se articula con el derecho al Habeas Data: la Ley Estatutaria 1581 de 2012 clasifica los datos biométricos como sensibles, y el Decreto 1377 de 2013 (Art. 6) establece que ninguna actividad puede condicionarse a que el titular los suministre. Esta teoría orienta el tercer objetivo específico, que valida que el prototipo cumpla estas condiciones.
```

### 5.2.2, reemplazar el texto
```
Código bidimensional cuyo contenido cambia a intervalos cortos. En este proyecto, el servidor genera un código numérico de seis dígitos que se renueva cada cinco segundos y acepta el código anterior durante tres segundos más, para tolerar la latencia de la red. Una captura de pantalla reenviada deja de ser válida en pocos segundos, lo que dificulta el registro desde fuera del aula (Canico Hernández et al., 2024; Nwabuwe et al., 2023).
```

### 5.2.3, reemplazar el texto
```
Tecnología que identifica a una persona comparando los rasgos de su rostro con una plantilla registrada previamente. Se complementa con una prueba de vida, que verifica que frente a la cámara hay una persona real y no una fotografía o una pantalla. En la prueba de vida activa, el sistema pide un gesto aleatorio, como parpadear o sonreír, y lo valida dentro de un tiempo límite (Cano Perfecto et al., 2026).
```

### 5.2.4, título:
```
5.2.4 GEOCERCA Y GEOLOCALIZACIÓN GPS
```
Cambiar la primera frase del texto por:
```
Perímetro virtual definido por un radio en metros alrededor de la ubicación que registra el docente al abrir la sesión de asistencia.
```

### 5.2.5: ver el bloque de huella del dispositivo de la respuesta anterior
Título: **5.2.5 HUELLA DIGITAL DEL DISPOSITIVO (DEVICE FINGERPRINT)**
```
Técnica de seguridad que identifica el teléfono desde el cual se registra una asistencia sin acceder a identificadores restringidos como el IMEI. Consiste en combinar varias características del equipo y aplicarles una función hash, que convierte esos datos en un código de longitud fija del cual no es posible recuperar la información original. Si dos cuentas registran asistencia en la misma sesión con la misma huella, el sistema infiere que un mismo teléfono se usó para marcar a nombre de otra persona (Nwabuwe et al., 2023).
```

### 5.2.6: aplicar el estilo **Título 3** y cambiar la última parte
Cambiar "(Ley Estatutaria 1581 de 2012; Superintendencia de Industria y Comercio, 2025)" por:
```
(Ley Estatutaria 1581 de 2012; Decreto 1377 de 2013, Art. 6; Superintendencia de Industria y Comercio, 2018)
```

### 5.3.2: añadir al final
```
Una vez finalizada la clase, los docentes transcriben la asistencia al sistema académico institucional Banner [VERIFICAR: confirmar que este es el sistema y cómo se carga la asistencia].
```

### 5.3.3, corregir el cálculo de horas
Reemplazar "ocasiona una pérdida acumulada de entre 3 y 4 horas semanales" por:
```
ocasiona una pérdida acumulada de entre 60 y 80 minutos semanales de tiempo efectivo de enseñanza por cada grupo académico
```
Y reemplazar "En este entorno, la toma de asistencia manual consumía un promedio de 15 a 20 minutos" por:
```
En este entorno, la toma de asistencia manual consumía un promedio de [DATO] minutos, según el cronometraje realizado en el diagnóstico (ver Capítulo 7)
```
(Si el dato medido difiere, recalcular: minutos × 4 sesiones = minutos semanales.)

Cambiar también "garantizando una ruta alternativa de verificación no biométrica, mediante código QR dinámico y geocerca GPS" por:
```
lo que obliga a que el registro de asistencia no dependa de la entrega del rostro
```

---

## J. Marco legal (5.4)

### Párrafo introductorio, reemplazar:
```
Esta sección analiza las normas colombianas que regulan el derecho al Habeas Data, la protección de datos personales y el tratamiento de información biométrica, así como las que se relacionan con la educación superior, las tecnologías de la información y los delitos informáticos. Para cada norma se indica cómo se aplica al contexto de Unicatólica y cómo se tuvo en cuenta en el diseño del sistema.
```

### Nuevas entradas (pegar en este orden, antes de la Ley 1581)

**Constitución Política de Colombia de 1991, Artículo 15: Derecho a la intimidad y al Habeas Data**
```
Este artículo reconoce el derecho de todas las personas a su intimidad y a conocer, actualizar y rectificar la información que se haya recogido sobre ellas en bases de datos. Para el proyecto, es el fundamento del tratamiento de los datos de los estudiantes: el sistema les permite consultar y eliminar su plantilla facial desde la aplicación móvil.
```

### Ley 1581, añadir al final del párrafo
```
La Corte Constitucional, en la Sentencia C-748 de 2011, declaró exequible esta ley y precisó que el tratamiento de datos sensibles es excepcional.
```
Cambiar también "mediante código QR dinámico y geocerca GPS" por "mediante el registro manual por parte del docente" (o según la opción que elijan; ver el aviso al inicio).

**Decreto 1377 de 2013: Reglamentación parcial de la Ley 1581 de 2012** (pegar después de la Ley 1581)
```
Este decreto reglamenta la autorización del titular, las políticas de tratamiento y el tratamiento de datos sensibles. Su artículo 6 establece que ninguna actividad puede condicionarse a que el titular suministre datos personales sensibles. Para el proyecto, esto significa que el registro de asistencia no puede depender de la verificación facial: el estudiante que no autoriza el uso de su rostro debe poder quedar registrado por otra vía. El decreto también exige que el responsable del tratamiento, en este caso la institución, cuente con una política de tratamiento de datos y conserve prueba de la autorización.
```

**Concepto de la Superintendencia de Industria y Comercio, Radicación 18-171259 (2018)**
```
En este concepto, la SIC señala que la recolección de datos biométricos requiere la autorización escrita del titular y que no puede restringirse una actividad a la entrega de esos datos. Para el proyecto, confirma que la verificación facial debe ser voluntaria y que el aviso de privacidad debe aceptarse antes de registrar el rostro.
```

**Resolución 52185 de 2025 de la Superintendencia de Industria y Comercio**
```
En esta resolución, la SIC ordenó a un conjunto residencial de Bogotá que recolectaba datos biométricos con reconocimiento facial sin autorización suprimir esos datos y habilitar mecanismos de ingreso alternativos y no invasivos para quienes no autoricen su tratamiento. Aunque el caso no es académico, muestra cómo aplica la autoridad la norma: un sistema que use el rostro debe ofrecer otra vía y permitir la supresión de los datos. El prototipo incorpora ambas condiciones.
```

### Ley 1273: cambiar "(PostgreSQL/MySQL)" por "(PostgreSQL)"

### Ley 2502: reemplazar el párrafo
```
Esta ley modifica el artículo 296 del Código Penal (falsedad personal) y establece que, cuando la conducta se realice con herramientas de inteligencia artificial, la multa se aumentará hasta en una tercera parte. Su relevancia para el proyecto es que reconoce la suplantación mediante contenido sintético como una amenaza real. El prototipo incluye una prueba de vida activa por gesto, pero no se evaluó frente a videos o rostros generados con inteligencia artificial; esa evaluación queda como una limitación y un trabajo futuro.
```

---

## K. Metodología

### 6.2: reemplazos
- "la correspondencia con los cuatro objetivos específicos del proyecto" → "la correspondencia con los tres objetivos específicos del proyecto"
- "Asimismo, se emplea en la fase final del objetivo 4" → "Asimismo, se emplea en el objetivo 3"
- "Se ejecuta durante el diseño, construcción y validación del prototipo en los Objetivos 2, 3 y 4" → "Se ejecuta durante el diseño, la construcción y la validación del prototipo, en los objetivos 2 y 3"
- "orientado a reducir de 15-20 minutos a menos de 5 minutos por sesión" → "comparado con el tiempo del registro manual medido en el diagnóstico"

### 6.3: reemplazos
- "dar cumplimiento a los cuatro objetivos específicos" → "dar cumplimiento a los tres objetivos específicos"
- "(Node.js/Fastify, TypeScript, PostgreSQL, Redis, Docker y Vue.js 3)" → "(Node.js/Fastify, TypeScript, PostgreSQL, Docker, Vue 3 y React Native)"

### Tabla 1: reemplazar completa

| Objetivo específico | Información requerida | Técnica e instrumento | Método de análisis |
|---|---|---|---|
| Objetivo 1: Diagnosticar el proceso manual de control de asistencia | Tiempo del pase de lista, conductas de fraude en la asistencia, fallas operativas de las planillas | Cronometraje de sesiones, encuesta a estudiantes, entrevista semiestructurada a docentes, revisión de planillas | Estadística descriptiva (promedios y porcentajes) y categorización de vulnerabilidades |
| Objetivo 2: Diseñar e implementar la arquitectura, la base de datos y el prototipo | Requerimientos funcionales, casos de uso, modelo entidad-relación, reglas antifraude (QR dinámico, geocerca, huella del dispositivo, verificación facial) | Modelado UML, especificación de requerimientos, desarrollo con Fastify, Vue 3, React Native y PostgreSQL, contenedores Docker | Pruebas unitarias, verificación de integridad referencial y revisión del flujo de datos |
| Objetivo 3: Validar la viabilidad técnica, la usabilidad y el cumplimiento de la Ley 1581 de 2012 | Tiempos de marcaje, intentos de fraude bloqueados, falsos rechazos, usabilidad percibida, uso de la vía no biométrica | Prueba piloto, registros del servidor, cuestionario SUS, verificación de requisitos legales | Estadística descriptiva, puntaje SUS y matriz de cumplimiento normativo |

### 5.4 Tratamiento de la información (sección nueva, después de 6.3)

Si siguen la plantilla, va como 5.4. Si no, como 6.4.
```
6.4 TRATAMIENTO DE LA INFORMACIÓN

6.4.1 Técnicas estadísticas
Los datos cuantitativos se analizaron con estadística descriptiva: promedios y desviación estándar para los tiempos de pase de lista y de marcaje, y porcentajes para las respuestas de la encuesta, los intentos de fraude bloqueados y los falsos rechazos. La usabilidad se midió con la escala SUS (System Usability Scale), cuyo puntaje va de 0 a 100. Las entrevistas a docentes se analizaron por categorías: tiempo, confiabilidad del registro y seguimiento de las inasistencias.

6.4.2 Presentación de la información
Los resultados se presentan en tablas y figuras de elaboración propia, organizadas por objetivo específico en los Capítulos 7, 8 y 9. Los instrumentos de recolección se incluyen en los anexos.
```

---

## L. Desarrollo

### Capítulo 7: diagnóstico

**P0464**, reemplazar la frase final "Este resultado coincide con las métricas reportadas en la literatura…" por:
```
[Escribir cuando tengan el dato: comparar los minutos medidos con lo reportado por Canico Hernández et al. (2024) u otra fuente que dé una cifra.]
```

**P0490**, reemplazar a partir de "Esta cifra supera…" por:
```
Esta cifra [es mayor / es menor / es similar] al 35,4% que Mejía y Ordóñez (2004) registraron en la Universidad de los Andes.
```
(Quitar la comparación con el 89%: ese dato es de suplantación en exámenes.)

**7.1, primer punto**, reemplazar:
```
Necesidad de dinamismo temporal: se determinó que el código QR no puede ser estático; debe cambiar cada pocos segundos para que una captura reenviada deje de ser válida.
```

**7.1, tercer punto**, reemplazar:
```
Validación de identidad y dispositivo: se identificó la necesidad de reconocer el teléfono desde el cual se registra cada asistencia mediante una huella del dispositivo, y de ofrecer una verificación facial con prueba de vida que el docente pueda activar en cada sesión.
```

**7.1, cuarto punto**, reemplazar:
```
Cumplimiento normativo (Ley 1581 de 2012): para respetar la voluntariedad del tratamiento de datos biométricos, se definió que la verificación facial fuera opcional para el docente en cada sesión y que el estudiante que no autoriza el uso de su rostro pudiera quedar registrado por otra vía.
```

### Capítulo 8

**8.1, P0523 (arquitectura)**: usar el párrafo de la respuesta anterior (arquitectura cliente-servidor en capas). Título de la Figura 3:
```
Figura 3. Arquitectura cliente-servidor en capas del sistema
```

**8.1**: añadir después de la frase sobre Redis:
```
El backend y la base de datos se empaquetaron en contenedores Docker, definidos en archivos docker-compose para los entornos de desarrollo y producción.
```

**Tabla 4**: añadir una columna "Código" (M1 a M6) y reemplazar las dos filas de estudiante:

| Código | Módulo | Actor | Alcance |
|---|---|---|---|
| M1 | Autenticación y cuenta | Todos | (sin cambios) |
| M2 | Gestión docente | Docente | (sin cambios) |
| M3 | Estudiante, verificación facial | Estudiante (app móvil) | Registro de la plantilla facial con aceptación previa del aviso de privacidad; en sesiones con verificación facial: escaneo del QR, envío de la ubicación GPS y de la huella del dispositivo (device fingerprint), reto de gesto y envío del vector facial |
| M4 | Estudiante, registro sin biometría | Estudiante (app móvil) / Docente | Registro con QR dinámico, ubicación GPS y huella del dispositivo cuando la sesión no exige verificación facial; registro manual por el docente cuando la exige y el estudiante no autorizó su rostro |
| M5 | Administración general | Administrador | (sin cambios) |
| M6 | Reportes y alerta de inasistencia | Docente / Administrador | Consolidado de asistencia, exportación a Excel y alerta por 4 inasistencias consecutivas |

**8.3**, cambiar "Este esquema permite visualizar las 13 tablas" y la frase previa por:
```
En la Tabla 5 se detallan las 10 entidades principales; las 3 restantes son [VERIFICAR en las migraciones: por ejemplo, la de administradores, la de códigos de recuperación y la de aceptación de términos].
```

**Tabla 5**, fila `attendance_details`, columna de campos:
```
state_attendance (attended, no_attended, no_attended_excuse, suplanted), device_fingerprint, biometric_verified
```
Y añadir debajo de la tabla:
```
El estado suplanted se asigna cuando el estudiante marca desde fuera de la geocerca o cuando el mismo teléfono registra a más de una cuenta en la sesión. En ambos casos el registro queda guardado para que el docente lo revise.
```

**8.4.1**, reemplazar la frase del IMEI: usar el bloque 3 de la respuesta anterior (huella SHA-256, diez señales, Android ID / identifierForVendor).

**Tabla 6**, fila Sistema/API, cambiar:
- "verificar firma de QR dinámico" → "validar que el código QR esté vigente"
- "validar la huella del dispositivo" → "detectar huellas de dispositivo repetidas en la sesión"

**Tabla 8**: cambios
- Paso 1, "La API válida" → "La API valida"
- Paso 3, "La API valida token vigente" → "La API valida que el código de 6 dígitos esté vigente"
- Paso 4, reemplazar:
```
Si la sesión exige verificación facial (biometric_required = true) y la petición no trae el reto facial, la API responde 428 Precondition Required sin registrar nada. | La aplicación activa la cámara y presenta el reto de gesto. Si el estudiante no autorizó el uso de su rostro, el docente registra su asistencia manualmente (Tabla 7).
```
- Añadir una nota debajo de la tabla:
```
El registro de la plantilla facial es un paso previo e independiente del marcado: el estudiante acepta el aviso de privacidad y registra su rostro desde la aplicación (endpoint /api/student/biometrics/template). Durante el marcado, el vector capturado se compara con esa plantilla.
```

**Tabla 9**, "válida hash con bcrypt" → "valida el hash con bcrypt" y "(válida QR, GPS, fingerprint y vector facial)" → "(valida el código QR, la ubicación GPS, la huella del dispositivo y el vector facial)".

**8.5**, reemplazar los dos primeros puntos:
```
Eficiencia en infraestructura: el diseño ubicó el procesamiento del rostro en el teléfono del estudiante, con TensorFlow Lite y MobileFaceNet, de modo que el servidor solo compara dos vectores de 192 números y no necesita hardware especializado.

Separación de las vías de registro (Ley 1581 de 2012): la arquitectura separó el módulo de verificación facial (M3) del registro sin biometría (M4), de modo que la verificación facial pueda activarse o desactivarse por sesión y que el estudiante que no autoriza el uso de su rostro no quede excluido.
```
Y en el tercer punto, cambiar "demostró que se pueden gestionar" por "permitió gestionar".

**8.7**, reemplazar la frase de rotación:
```
El servidor genera un código numérico de seis dígitos y lo renueva cada cinco segundos; el docente puede configurar este intervalo entre 5 y 300 segundos. Para evitar rechazos por la latencia de la red, la API acepta el código anterior durante tres segundos adicionales.
```

**8.9**, reemplazar el párrafo de la ruta alternativa:
```
En cumplimiento de la Ley Estatutaria 1581 de 2012 y del Decreto 1377 de 2013, la verificación facial es opcional en dos niveles. Primero, el docente decide en cada sesión si la exige. Cuando no la exige, todos los estudiantes marcan con el código QR dinámico, la geocerca y la huella del dispositivo. Segundo, el estudiante decide si registra su rostro: antes de hacerlo debe aceptar el aviso de privacidad, y puede consultar o eliminar su plantilla en cualquier momento desde la aplicación. Si una sesión exige verificación facial y el estudiante no autorizó el uso de su rostro, el docente registra su asistencia manualmente, de modo que la entrega del rostro no condiciona el registro.
```

**8.10**, reemplazar el párrafo del algoritmo de alerta:
```
Se programó una alerta temprana de inasistencia. El sistema cuenta, desde la sesión más reciente hacia atrás, las inasistencias consecutivas de cada estudiante en cada asignatura, y lo muestra en el panel del docente cuando acumula cuatro. Se cuenta como inasistencia cualquier registro distinto de "asistió", incluidas las faltas justificadas y los registros marcados como suplantación. La racha se reinicia con la primera asistencia. Esta alerta identifica el riesgo de pérdida de la asignatura por inasistencia, que es uno de los factores asociados a la deserción. [VERIFICAR: comparar el umbral de 4 faltas con el porcentaje de inasistencia que fija el Reglamento Estudiantil de Unicatólica.]
```
Título de la Figura 10:
```
Figura 10. Panel de alertas tempranas por inasistencia
```

**Tabla 10**, cambiar:
- Generador QR, "Rotación automática cada 10s con búfer de 3s" → "Rotación automática cada 5 s (configurable) con tolerancia de 3 s"
- Columna "Estado de construcción": cambiar todos los "100% Codificado/Desplegado/Funcional" por "Implementado"
- Ruta no biométrica, "Marcado seguro mediante QR + GPS + Fingerprint sin uso de cámara" → "Marcado con QR, GPS y huella del dispositivo cuando la sesión no exige verificación facial"

**P0659 (cierre del Capítulo 8)**, reemplazar:
```
Con los siete componentes integrados, el prototipo pasó a la fase de pruebas piloto del tercer objetivo. La separación entre el registro con verificación facial y el registro sin biometría permitió que el uso del rostro fuera voluntario, como exige la legislación colombiana sobre datos sensibles.
```

### Capítulo 9

**9.1**, añadir al final:
```
Para las pruebas, el radio de la geocerca se configuró en 20 metros [VERIFICAR] y el umbral de similitud facial en 0,75. El intervalo de rotación del código QR se mantuvo en el valor por defecto de cinco segundos.
```

**Tabla 11**, título:
```
Tabla 11. Tiempos promedio de ejecución por componente y tiempo total de marcaje
```
En la columna "Grado de cumplimiento", cambiar "Excedido satisfactoriamente", "Cumplido ampliamente" y "Meta cumplida al 100%" por "Cumplido".

**9.2**, cerrar el párrafo:
```
…lo que representó una reducción del [DATO]% frente a los [DATO] minutos del método manual medidos en el Capítulo 7.
```
Fórmula: reducción = (minutos manuales − 3,2) / minutos manuales × 100.

**9.3**, primer párrafo, lista de escenarios (para que coincida con la tabla):
```
Se simularon cinco escenarios de fraude: reenvío de una captura del código QR vencido, marcado desde fuera del aula, suplantación del rostro con una fotografía impresa o en pantalla, uso del mismo teléfono por dos estudiantes y envío de un vector facial alterado.
```

**Tabla 12**, filas corregidas:

| Escenario | Intentos | Bloqueados | Efectividad | Respuesta del sistema |
|---|---|---|---|---|
| Reenvío de captura del QR vencido (más de 5 s más 3 s de tolerancia) | 50 | 50 | 100,0% | HTTP 400 (código inválido o expirado) |
| Marcado fuera del aula (más de 20 metros) | 40 | 40 | 100,0% | Registro con estado suplanted |
| Mismo teléfono usado por dos estudiantes | 30 | 30 | 100,0% | Ambos registros con estado suplanted |
| Rostro con fotografía impresa o en pantalla | 15 | 14 | 93,3% | HTTP 403 (prueba de vida fallida o similitud menor que 0,75) |
| Vector facial alterado | 10 | 10 | 100,0% | Rechazo por similitud menor que 0,75 |
| **Total** | **145** | **144** | **99,3%** | |

[VERIFICAR: en el escenario del QR vencido, confirmar que en las pruebas el intervalo era de 5 s y no de 10 s.]

**P0702**, reemplazar:
```
Los resultados de la Tabla 12 muestran que la combinación de controles bloqueó 144 de los 145 intentos de fraude simulados (99,3%). Todos los intentos de marcar desde fuera del aula y de usar el mismo teléfono para dos estudiantes quedaron registrados como suplantación. El único intento que superó los controles fue una suplantación del rostro con fotografía o pantalla, lo que indica que la prueba de vida por gesto es el control más débil. Estos resultados provienen de ataques simulados por el equipo del proyecto y no de intentos de fraude reales.
```

**9.4**, título:
```
9.4 VERIFICACIÓN DEL CUMPLIMIENTO DE LA LEY 1581 DE 2012 Y USO DE LA VÍA SIN BIOMETRÍA
```
Primera frase: "Un componente central del objetivo 4" → "Un componente central del tercer objetivo". "los cuatro principios rectores" → "los principios de la Ley 1581 de 2012 aplicables al tratamiento de datos biométricos".

**Tabla 13**, reemplazar completa:

| Principio o exigencia | Exigencia normativa | Mecanismo implementado | Estado |
|---|---|---|---|
| Libertad (Art. 4, lit. c) | El tratamiento requiere autorización previa, expresa e informada | Aviso de privacidad y aceptación explícita antes de registrar el rostro | Implementado |
| No condicionamiento (Decreto 1377, Art. 6) | Ninguna actividad puede condicionarse a la entrega de datos sensibles | Verificación facial opcional por sesión; registro manual por el docente para quien no autoriza su rostro | Implementado |
| Finalidad (Art. 4, lit. b) | Los datos se usan solo para el fin autorizado | La plantilla facial se usa solo para verificar la asistencia | Implementado |
| Seguridad (Art. 4, lit. g) | Proteger los datos contra acceso no autorizado | El rostro se procesa en el teléfono y no se envían fotografías; la plantilla de 192 valores se guarda en el servidor con acceso restringido por rol [VERIFICAR si está cifrada en reposo] | Implementado parcialmente |
| Acceso y circulación restringida (Art. 4, lit. f) | Solo personas autorizadas acceden a los datos | Control de acceso por roles (docente, estudiante, administrador) con JWT | Implementado |
| Supresión (Art. 8, lit. e) | El titular puede pedir la eliminación de sus datos | El estudiante puede consultar y eliminar su plantilla desde la aplicación | Implementado |
| Transparencia (Art. 4, lit. e) | El titular puede conocer qué datos suyos se tratan | El estudiante puede consultar el estado de su registro biométrico | Implementado |
| Responsable y política de tratamiento (Decreto 1377) | La institución debe tener una política de tratamiento | Depende de Unicatólica; fuera del alcance del prototipo | Pendiente institucional |

Debajo de la tabla, añadir los datos de la prueba:
```
Durante la prueba piloto, [DATO] de los 64 estudiantes registraron su rostro y [DATO] prefirieron no hacerlo. [DATO] estudiantes fueron registrados manualmente por el docente en sesiones con verificación facial.
```

**P0708 (cierre del Capítulo 9)**, reemplazar:
```
Los resultados del tercer objetivo mostraron que el prototipo redujo el pase de lista a 3,2 minutos por grupo, bloqueó el 99,3% de los intentos de fraude simulados y obtuvo [DATO] puntos en la escala SUS. La verificación facial opcional y el registro sin biometría permitieron cumplir la exigencia legal de no condicionar la asistencia a la entrega del rostro. La adopción institucional requiere, además, que Unicatólica defina su política de tratamiento de datos biométricos.
```

**9.5 EVALUACIÓN DE USABILIDAD** (sección nueva)
```
9.5 EVALUACIÓN DE USABILIDAD

Al finalizar la prueba piloto se aplicó el cuestionario SUS (System Usability Scale) a [DATO] estudiantes y a los 3 docentes. El cuestionario tiene diez afirmaciones con una escala de 1 a 5, y su resultado se convierte en un puntaje de 0 a 100; un puntaje de 68 o más se considera superior al promedio. El instrumento se incluye en el Anexo [letra].

Los estudiantes obtuvieron un puntaje promedio de [DATO] (desviación estándar [DATO]) y los docentes de [DATO]. [Interpretar: qué afirmaciones tuvieron mejor y peor calificación.]

Además, se midieron los rechazos de usuarios legítimos: la geocerca rechazó a [DATO] estudiantes que sí estaban en el aula, con un error de ubicación promedio de [DATO] metros, y la verificación facial rechazó [DATO] de [DATO] intentos de estudiantes registrados (similitud menor que 0,75).
```

---

## M. Estructura y numeración

**Opción 1 (recomendada, sigue la plantilla)**: mover el Estado del arte dentro del Marco referencial.
```
4. MARCO REFERENCIAL
4.1 ESTADO DEL ARTE (4.1.1 Internacional, 4.1.2 Nacional, 4.1.3 Local)
4.2 MARCO TEÓRICO
4.3 MARCO CONCEPTUAL
4.4 MARCO CONTEXTUAL
4.5 MARCO LEGAL
5. METODOLOGÍA (5.1 a 5.4)
6. DESARROLLO PRIMER OBJETIVO
7. DESARROLLO SEGUNDO OBJETIVO
8. DESARROLLO TERCER OBJETIVO
9. CONCLUSIONES
10. RECOMENDACIONES
BIBLIOGRAFÍA
ANEXOS
```
**Opción 2**: dejar el Estado del arte como Capítulo 4, solo si el director lo aprueba.

En ambos casos: quitar el "4." de BIBLIOGRAFÍA, numerar 1.1, 1.2 y 2.1 a 2.5, y regenerar la tabla de contenido y las listas desde Referencias → Actualizar tabla.

**Anexos** (sección nueva):
```
ANEXOS
Anexo A. Encuesta aplicada a estudiantes
Anexo B. Guion de entrevista a docentes
Anexo C. Formato de cronometraje del pase de lista
Anexo D. Cuestionario SUS
Anexo E. Aviso de privacidad y autorización de tratamiento de datos biométricos
```

---

## N. Bibliografía

Usar la lista corregida de la sección 8 de `Revision coherencia - Trabajo de grado.md`. Además, añadir:
```
Corte Constitucional de Colombia. (2011, 6 de octubre). Sentencia C-748 de 2011 (M.P. Jorge Ignacio Pretelt Chaljub).
```
(Ya está en la bibliografía; ahora se cita en el Marco legal.)

Y cambiar en todo el texto:
- "Cano-Perfecto et al." → "Cano Perfecto et al."
- "Canico et al." → "Canico Hernández et al."
- "Hurtado-Pardo y Llanos-Bermúdez" → "Hurtado Pardo y Llanos Bermúdez"
- "(Superintendencia de Industria y Comercio, 2025)" → "(Superintendencia de Industria y Comercio, 2018)" cuando se refiere al concepto, o "(Superintendencia de Industria y Comercio, 2025)" solo cuando se refiere a la Resolución 52185.
- Decimales con coma: 35,4%; 99,3%; 93,3%.

---

## O. Estilo (búsquedas con Ctrl+B en Word)

| Buscar | Reemplazar por |
|---|---|
| "elimina la suplantación" | "reduce la suplantación" |
| "erradica" / "erradicando" | "bloquea" / "bloqueando" |
| "100%" (fuera de las tablas de resultados) | quitar |
| "en estricto cumplimiento" | "en cumplimiento" |
| "de forma contundente" | quitar |
| "Asimismo," | dejar máximo 4 en todo el documento |
| "En este contexto," | quitar en la mayoría |
| "garantiza" | "asegura", "permite" o el verbo concreto |
