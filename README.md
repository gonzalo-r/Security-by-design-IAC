# Security-by-design-IAC
El formulario IaC busca entender la capacidad operativa y el alcance de ejecución del código sobre la infraestructura.

Lo completaría el responsable técnico, DevOps, Infraestructura, Cloud Engineer o quien desarrolla y mantiene los playbooks.

Bloque A. Identificación y propósito
#	Pregunta	Objetivo
1	¿Cuál es el nombre del proyecto, repositorio o automatización?	Identificación
2	¿Quién es el responsable técnico y quién aprueba su ejecución?	Responsabilidad
3	¿Qué tecnología utiliza?	Ansible, Terraform, OpenTofu, CloudFormation, etc.
4	¿Es una nueva automatización o una modificación de una existente?	Alcance del cambio
5	¿Cuál es el objetivo de la automatización y qué tareas realiza?	Entender su función

Bloque B. Alcance e impacto sobre infraestructura
Este es uno de los bloques más importantes.
#	Pregunta	Objetivo
6	¿Qué infraestructura o recursos administra?	Servidores, redes, bases de datos, servicios cloud, contenedores, etc.
7	¿Sobre qué ambientes puede ejecutarse?	Desarrollo, QA, Preproducción, Producción
8	¿La automatización tiene alcance sobre infraestructura productiva?	Impacto
9	¿Cuántos recursos o activos puede modificar aproximadamente?	Alcance / blast radius
10	¿Puede modificar configuraciones de seguridad, firewall, IAM, accesos, redes o políticas?	Impacto en controles de seguridad
11	¿Puede eliminar, reiniciar, reemplazar o modificar recursos existentes?	Riesgo de indisponibilidad

Bloque C. Privilegios y accesos
Para mí, este bloque debería tener especial peso en la clasificación.
#	Pregunta	Objetivo
12	¿Con qué identidad o cuenta se ejecuta la automatización?	Identidad de ejecución
13	¿Qué nivel de privilegios requiere?	Usuario estándar, sudo, root, administrador cloud
14	¿Utiliza credenciales, claves SSH, tokens o cuentas de servicio?	Gestión de credenciales
15	¿Dónde se almacenan y cómo se protegen los secretos?	Vault, Secrets Manager, variables protegidas, archivos, etc.
16	¿La automatización puede crear, modificar o eliminar usuarios, roles, permisos o credenciales?	Riesgo de escalamiento de privilegios

Bloque D. Ejecución y gobierno
#	Pregunta	Objetivo
17	¿Desde dónde se ejecuta?	AWX, Ansible Tower, Jenkins, GitLab, ADO, ejecución manual, etc.
18	¿La ejecución requiere aprobación previa?	Control de cambios
19	¿Existe revisión del código antes de ejecutar?	Peer review
20	¿Se registra quién ejecutó la automatización, cuándo y sobre qué activos?	Trazabilidad
21	¿Existe un mecanismo de rollback o recuperación ante una ejecución incorrecta?	Resiliencia

No necesariamente todas las preguntas tienen que ser obligatorias para todos los tipos de IaC. Algunas pueden habilitar preguntas condicionales.

Ansible – Configuration Management

Evaluar qué configura, sobre qué equipos actúa, con qué privilegios y qué cambios puede producir.

Ejemplo: un playbook que modifica SSH, usuarios, firewall o actualiza paquetes en servidores productivos.

Terraform – Infrastructure Provisioning

Evaluar qué recursos crea, modifica o destruye, permisos del provider, estado, módulos, dependencias y exposición de recursos.

Ejemplo: un Terraform que crea una VPC, modifica Security Groups o asigna permisos IAM.

Bloque común	Ansible	Terraform
Identificación	Playbook / Roles	Modules / Workspaces
Alcance	Hosts y grupos	Recursos y providers
Privilegios	SSH, sudo, root	IAM, service principals
Secretos	Ansible Vault	Variables, backend, secrets
Ejecución	AWX, CI/CD, CLI	Plan / Apply, CI/CD
Impacto	Cambios sobre sistemas	Creación, modificación y destrucción
Trazabilidad	Logs de ejecución	State, plan y auditoría
Recuperación	Rollback / configuración previa	State / recuperación de recursos

Qué controles debería exigir Seguridad
El formulario no debería limitarse a recolectar información. Tiene que alimentar una evaluación técnica y definir qué controles serán obligatorios.

Por ejemplo:
Control	Aplicación
Revisión de código	Obligatoria
Protección de ramas y aprobación	Obligatoria
Escaneo de secretos	Obligatorio
Análisis estático de IaC	Según tecnología
Validación de configuraciones inseguras	Obligatoria
Gestión segura de credenciales	Obligatoria
Segregación de ambientes	Según alcance
Control de privilegios	Obligatorio
Aprobación de ejecución productiva	Según criticidad
Evidencia de ejecución	Obligatoria

1. Secure IaC – Infraestructura: formulario para perfiles técnicos, evaluación de privilegios, alcance e impacto operativo.
2. Cambios de infraestructura existentes: evaluación proporcional cuando se modifica una automatización ya aprobada.

 Solicitud técnica

Formulario de IaC

Triage de Seguridad

Clasificación y análisis de impacto

Definición de controles

Requisitos según criticidad

Validación técnica

Análisis, revisión y evidencias

Aprobación / Excepción / Remediación

Registro y seguimiento del riesgo

el proceso debe ser proporcional. No podemos exigir el mismo análisis para un playbook que actualiza un paquete en un servidor de desarrollo que para uno que modifica IAM, firewalls y servidores de producción.

Esto también te permite formalizar la responsabilidad técnica, la revisión de cambios y la aceptación de riesgos por parte de los responsables correspondientes.

El presente formulario tiene como objetivo relevar las características técnicas, el alcance operativo y los mecanismos de ejecución de las automatizaciones desarrolladas mediante Ansible, a fin de identificar riesgos de seguridad y determinar los controles necesarios para su implementación segura.
Bloque 1. Identificación de la automatización
1. ¿Cuál es el nombre de la automatización o proyecto?

- Respuesta abierta.

2. ¿Cuál es el repositorio donde se encuentra alojado el código?

- URL del repositorio.

3. ¿Quién es el responsable técnico de la automatización?

- Nombre y equipo responsable.

4. ¿Qué tipo de desarrollo estás implementando?
- Nuevo Playbook.
- Modificación de Playbook existente.
- Nuevo Role.
- Modificación de Role existente.
- Automatización de infraestructura existente.
- Otro.
5. ¿Cuál es el objetivo principal de la automatización?

- Respuesta abierta. Describir brevemente qué tareas realiza.
Bloque 2. Alcance operativo
6. ¿Qué tipo de infraestructura administra o modifica la automatización?
- Servidores Linux.
- Servidores Windows.
- Servicios Cloud (AWS, Azure, OCI, etc.).
- Bases de datos.
- Redes y dispositivos de infraestructura.
- Contenedores / Kubernetes.
- Configuración de servicios y aplicaciones.
- Otro.
7. ¿Sobre qué ambientes se ejecutará?
- Desarrollo.
- Testing / QA.
- Preproducción.
- Producción.
- Múltiples ambientes.
8. ¿Cuál es el alcance aproximado de ejecución?
- Un único servidor o recurso.
- Entre 2 y 10 servidores.
- Entre 11 y 50 servidores.
- Entre 51 y 100 servidores.
- Más de 100 servidores.
- Infraestructura dinámica o variable.
9. ¿La automatización puede modificar componentes que soportan servicios críticos para el negocio?
- Sí.
- No.
- No lo sé.
10. ¿Qué tipo de acciones realiza la automatización?
- Instalación o actualización de paquetes.
- Modificación de configuraciones.
- Alta, baja o modificación de usuarios.
- Gestión de permisos y privilegios.
- Configuración de firewall y redes.
- Gestión de servicios y procesos.
- Modificación de parámetros de seguridad.
- Creación o eliminación de infraestructura.
- Ejecución de comandos o scripts.
- Otra.
Bloque 3. Privilegios y permisos
11. ¿Con qué nivel de privilegios se ejecutan los Playbooks?
- Usuario estándar.
- Usuario con permisos sudo.
- Root / Administrador.
- Cuenta de servicio con privilegios específicos.
- Credenciales de administrador de infraestructura.
- No lo sé.
12. ¿La automatización puede crear, modificar o eliminar usuarios, grupos, permisos o cuentas de servicio?
- Sí.
- No.
13. ¿La automatización tiene capacidad para modificar controles de seguridad?

Por ejemplo: SSH, firewall, antivirus/EDR, políticas de acceso, auditoría, hardening o configuraciones de seguridad.
- Sí.
- No.
- No lo sé.
14. ¿Qué mecanismos de autenticación utiliza para conectarse a los equipos administrados?
- SSH con claves.
- SSH con usuario y contraseña.
- WinRM.
- Cuentas de servicio.
- Credenciales de Cloud.
- Otros.
Bloque 4. Gestión de secretos y credenciales
15. ¿La automatización utiliza información sensible o credenciales?
- Contraseñas.
- Claves privadas SSH.
- Tokens de acceso.
- Credenciales Cloud.
- Certificados.
- No utiliza credenciales.
- Otros.
16. ¿Dónde se almacenan las credenciales y secretos utilizados?
- Ansible Vault.
- Secret Manager / Vault corporativo.
- Variables protegidas del pipeline.
- AWX / Ansible Tower Credentials.
- Archivos de configuración.
- Variables de entorno.
- Código fuente del repositorio.
- Otro.
17. ¿Los secretos se encuentran protegidos contra su exposición en logs, salidas de ejecución o repositorios?
- Sí.
- No.
- No lo sé.
Bloque 5. Ejecución y control de cambios
18. ¿Desde dónde se ejecutan los Playbooks?
- AWX / Ansible Tower.
- Jenkins.
- Azure DevOps.
- GitLab CI/CD.
- Ejecución manual desde terminal.
- Otro.
19. ¿Existe una revisión del código por otra persona antes de su ejecución?
- Sí, mediante Pull Request / Merge Request.
- Sí, mediante revisión formal.
- No, lo ejecuta directamente el desarrollador.
- Depende del tipo de cambio.
20. ¿La ejecución sobre producción requiere aprobación previa?
- Sí.
- No.
- Depende del tipo de automatización.
21. ¿Existe registro de las ejecuciones realizadas?
- Sí, con identificación del usuario, fecha, hora y resultado.
- Sí, pero con información parcial.
- No.
22. ¿Existe algún mecanismo para validar los cambios antes de ejecutarlos?
- Sí, mediante Check Mode (--check).
- Sí, mediante ejecución en ambiente de prueba.
- Sí, mediante validaciones automatizadas.
- No.
- Otro.
23. ¿Existe un mecanismo de recuperación ante una ejecución incorrecta?
- Sí, rollback automatizado.
- Sí, procedimiento manual documentado.
- Sí, backup o snapshot previo.
- No.
- No aplica.

- Qué resultado debería generar el formulario
El formulario debería alimentar tu circuito DevSecOps y producir:
- Identificación del responsable técnico.
- Clasificación de criticidad.
- Alcance de infraestructura afectada.
- Nivel de privilegios.
- Requisitos de seguridad aplicables.
- Controles pendientes de implementación.
- Necesidad de revisión especializada por Seguridad.
- Evidencias requeridas para la aprobación.
