IA UTILIZADA: Gemini



Prompt utilizado:

De este enunciado: ... ¿Que ambigüedades encontras? Ya que lo voy a usar para hacer QA. Enumeralas, y dame un enunciado final que agregues estos requerimientos no definidos.



Para un analista de QA, las ambigüedades son "bugs" potenciales antes de que se escriba el código. En el enunciado actual, hay varios puntos ciegos técnicos y funcionales que podrían generar inconsistencias.

Aquí tienes el desglose de las ambigüedades y la propuesta de enunciado corregido:



1\. Ambigüedades Detectadas

&#x20;   •	Lógica de porcentajes: El texto dice que "siempre debe ser 100%". Si el usuario carga al primer beneficiario, ¿el sistema le pone 100% por defecto o le permite poner un valor menor y lo bloquea al guardar? Además, si se habilitan los otros beneficiarios para edición, ¿qué pasa si el usuario los modifica y la suma da 105%? Falta definir la validación en tiempo real.

&#x20;   •	Sexo y CUIT: Se define "Sexo" como Checkbox. Un checkbox suele ser binario (sí/no). Para generar un CUIT, se requiere una opción excluyente (Masculino/Femenino/Otro). Si es un checkbox único, no queda claro cómo se mapea al algoritmo de CUIT.

&#x20;   •	Campos bloqueados vs. Actualización: Si la persona ya existe y los campos se bloquean, ¿qué sucede si el domicilio registrado es viejo? El enunciado no prevé un mecanismo para solicitar actualización de datos si están desactualizados en el sistema central.

&#x20;   •	Formatos y Máscaras: No se especifican longitudes mínimas/máximas para "Número de documento" o "CUIL", ni el formato de la "Fecha de Nacimiento" (¿DD/MM/AAAA?).

&#x20;   •	Validación de Edad: Dice "de 1940 en adelante", pero no establece un límite superior. ¿Puede un recién nacido ser beneficiario? ¿Puede serlo alguien que aún no nació?

&#x20;   •	Estado de "Persona Viva": El enunciado dice que si la persona existe "se da por sentado que está viva". En QA, esto es un riesgo: ¿qué pasa si el servicio de búsqueda devuelve que la persona falleció?

&#x20;   •	Nacionalidad y Domicilio: No se definen los valores posibles para el desplegable de Nacionalidad ni para las Provincias/Países.

