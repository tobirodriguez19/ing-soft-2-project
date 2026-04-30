**GRUPO: CHICCARELLO FEDERICO y RODRIGUEZ TOBIAS**





Podemos realizar más casos de test que no detectó la IA. Como por ejemplo:



ID: TC\_DAT\_003

Título: Bloquear edición de datos autocompletados

Descripción: Verificar que los campos autocompletados de una persona existente no se puedan modificar.



ID: TC\_DAT\_004

Título: Campo CUIT no obligatorio para tipo DNI

Descripción: Validar que el CUIT no sea requerido cuando el tipo de documento es distinto de DNI.



ID: TC\_VAL\_003

Título: Validación de formato de número de documento (Negativo)

Descripción: El sistema rechaza formatos que inválidos de número de documento.



ID: TC\_VAL\_004

Título: Validación de fecha de nacimiento futura (Negativo)

Descripción: No debe permitir ingresar fechas posteriores a la actual.



ID: TC\_PCT\_004

Título: Edición de porcentaje en beneficiarios existentes

Descripción: Permite modificar porcentajes cuando un beneficiario ya existe.



ID: TC\_PCT\_005

Título: Validación de porcentaje mayor a 100 (Negativo)

Descripción: No permite ingresar valores individuales superiores al 100%.



ID: TC\_SAVE\_002

Título: Cancelación de alta de beneficiario

Descripción: Al cancelar, no se persisten los datos ingresados.

