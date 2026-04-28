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



\-----------------------------------------------------------------------------------------------------------

2\. Enunciado Final Refinado (QA Ready)

A continuación, el enunciado con las reglas de negocio normalizadas y las ambigüedades resueltas:

Funcionalidad: Alta de Beneficiarios en Seguro de Vida

&#x20; 1. Control de Acceso (Pre-condiciones):

&#x20;     •	El sistema permitirá buscar una cuenta por número.

&#x20;     •	Regla de Visibilidad: El botón "Alta de Beneficiario" solo será visible si el estado de la póliza es Activo. Si el estado es Suspendido o Dada de Baja, el botón debe estar oculto o deshabilitado con un tooltip explicativo.

&#x20; 2. Búsqueda y Autocompletado:

&#x20;     •	Al ingresar Tipo y Número de documento, el sistema consultará la base de datos central.

&#x20;     •	Si el registro existe: Se autocompletarán todos los campos de "Datos Personales" y "Domicilio". Estos campos pasarán a estado Solo Lectura (Disabled), excepto el "Porcentaje de Beneficio".

&#x20;     •	Si el registro no existe: Todos los campos marcados como obligatorios deberán quedar editables y vacíos.

&#x20; 3. Reglas de Campos y Validación:

&#x20;     •	Datos Personales (Obligatorios):

&#x20;         o	Tipo Documento: Desplegable (Valores: ET, PAS, CE, DNI, CL).

&#x20;         o	Fecha de Nacimiento: Formato DD/MM/AAAA. Rango válido: 01/01/1940 hasta \[Fecha Actual].

&#x20;         o	Sexo: Selector excluyente (Radio Button) para Masculino/Femenino (necesario para cálculo de CUIT).

&#x20;         o	CUIT: Campo numérico (11 dígitos).

&#x20;             	Auto-generación: Si Tipo = DNI, se calcula automáticamente al tener Documento + Sexo.

&#x20;             	Condición: Si Tipo != DNI, el campo es editable y opcional.

&#x20;         o	Discapacidad: Checkbox (Default: No marcado).

&#x20;     •	Domicilio (Obligatorios): Calle, Número, Código Postal, Localidad, Provincia (Desplegable), País (Desplegable). Nota: "Piso" es opcional.

&#x20; 4. Regla de Oro: Distribución de Beneficio:

&#x20;     •	El porcentaje individual debe ser mayor a 0.

&#x20;     •	La suma total de los porcentajes de todos los beneficiarios de la póliza debe ser exactamente 100% para permitir el guardado.

&#x20;     •	Comportamiento dinámico: Si al intentar cargar un nuevo beneficiario la suma total supera el 100%, el sistema debe habilitar la edición de los porcentajes de los beneficiarios existentes en la misma pantalla para permitir el reajuste antes de guardar.

&#x20; 5. Confirmación y Errores:

&#x20;     •	Validación al Guardar: El sistema verificará integridad de formatos (ej. CUIT válido), obligatoriedad y la regla del 100%.

&#x20;     •	Errores: Se mostrarán mensajes de error específicos (Inline) bajo cada campo inválido y un resumen superior.

&#x20;     •	Éxito: Se mostrará un mensaje de "Alta Exitosa" y se redirigirá automáticamente a la "Grilla de Beneficiarios" actualizada.

&#x20; 6. Tablas de Referencia:

&#x20;     •	IVA: Consumidor Final, Exento, Inscripto, Monotributista, No Categorizado, Sin Condición.

&#x20;     •	Estado Civil: Casado, Convivencia, Divorciado, Otros, Separado de hecho, Separado legal, Soltero, Unión de hecho, Viudo.



