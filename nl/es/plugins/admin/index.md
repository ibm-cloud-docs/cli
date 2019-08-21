---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-12"

keywords: cli, ibmcloud admin cli, admin cli plugin, admin plugin, cloud foundry admin cli plugin, adding users, buildpack, security groups, cf ba

subcollection: cloud-cli

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:note: .note}
{:important: .important}
{:tip: .tip}

# CLI de administración de {{site.data.keyword.cloud_notm}}
{: #ibmcloud-admincli}

Puede gestionar el entorno de {{site.data.keyword.cloud_notm}} Local o {{site.data.keyword.cloud_notm}} Dedicado mediante la interfaz de línea de mandatos de Cloud Foundry con el plugin de CLI de administración de {{site.data.keyword.cloud_notm}}. Por ejemplo, puede añadir usuarios de un registro de LDAP.

Antes de empezar, instale la CLI de Cloud Foundry. El plugin de CLI de administración de {{site.data.keyword.cloud_notm}} necesita `cf` versión 6.11.2 o posterior. [Descargar la interfaz de línea de mandatos de Cloud Foundry](https://github.com/cloudfoundry/cli/releases){: new_window} ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo").

Cygwin no admite la CLI de Cloud Foundry. Utilice la CLI de Cloud Foundry de en una ventana de línea de mandatos que no sea la ventana de Cygwin.

La CLI de administración de {{site.data.keyword.cloud_notm}} solo se utiliza para el entorno {{site.data.keyword.cloud_notm}} local y el entorno {{site.data.keyword.cloud_notm}} dedicado. No está soportado por {{site.data.keyword.cloud_notm}} Público.
{: note}

## Adición del plugin de CLI de administración de {{site.data.keyword.cloud_notm}}
{: #add-admin-cli}

Una vez instalada la CLI de Cloud Foundry, puede añadir el plugin de CLI de administración de {{site.data.keyword.cloud_notm}}.

Si ha instalado anteriormente el plugin de administración de {{site.data.keyword.cloud_notm}}, es posible que tenga que desinstalarlo, suprimir el repositorio y, a continuación, volver a instalarlo para obtener las actualizaciones más recientes.
{: tip}

Siga estos pasos para añadir el repositorio e instalar el plug-in:

1. Para añadir el repositorio de plugins de administración de {{site.data.keyword.cloud_notm}}, ejecute el siguiente mandato:
  ```
  cf add-plugin-repo IBMCloudAdmin https://<customer_console_endpoint>.bluemix.net/cli
  ```
  {: codeblock}

  Puede encontrar el mismo mandato con el punto final real en su página CLI de consola de administración:
`https://<customer_console_endpoint>.bluemix.net/cli`.
  {: note}

2. Para instalar el plugin de CLI de administración de {{site.data.keyword.cloud_notm}}, ejecute el mandato siguiente:
  ```
  cf install-plugin IBMCloudAdminCLI -r IBMCloudAdmin
```
  {: codeblock}

## Desinstalación del plugin de CLI de administración de {{site.data.keyword.cloud_notm}}
{: #remove-admin-cli}

Siga los siguientes pasos para desinstalar el plugin. 

1. Desinstale el plugin:
  ```
  cf uninstall-plugin IBMCloudAdminCLI
  ```
  {: codeblock}

2. Elimine el repositorio de plugins:
  ```
  cf remove-plugin-repo IBMCloudAdmin
  ```
  {: codeblock}

A continuación, puede añadir el repositorio actualizado e instalar el plugin más reciente.

## Utilización del plugin de la CLI de administración de {{site.data.keyword.cloud_notm}}
{: #using-admin-cli}

Puede utilizar el plugin de CLI de administración de {{site.data.keyword.cloud_notm}} para añadir o eliminar usuarios, asignar o desasignar usuarios de organizaciones y para realizar otras tareas de gestión.

Para ver una lista de mandatos, ejecute el mandato siguiente:
```
cf plugins
```
{: codeblock}

Para obtener más ayuda sobre un mandato, utilice la opción `-help`.

### Conexión e inicio de sesión en {{site.data.keyword.cloud_notm}}
{: #connecting-ibm-cloud}

1. Para conectar con el punto final de la API de {{site.data.keyword.cloud_notm}}, ejecute este mandato:
  ```
  cf api api.us-south.cf.cloud.ibm.com
  ```
  {: codeblock}
  
  Aunque los puntos finales de API de Cloud Foundry `api.*.bluemix.net` heredados siguen estando disponibles, puede actualizar los scripts y la automatización de infraestructura para que utilicen los puntos finales de API de Cloud Foundry actualizados siguientes para su región:

  * api.us-south.cf.cloud.ibm.com (anteriormente api.ng.bluemix.net)
  * api.eu-gb.cf.cloud.ibm.com (anteriormente api.eu-gb.bluemix.net)
  * api.us-east.cf.cloud.ibm.com (anteriormente api.us-east.bluemix.net)
  * api.eu-de.cf.cloud.ibm.com (anteriormente api.eu-de.bluemix.net)
  * api.au-syd.cf.cloud.ibm.com (anteriormente api.au-syd.bluemix.net)

  Puede consultar la página de Recursos e información de la consola de administración para obtener el URL correcto. El URL se muestra en la sección de información de la API en el campo **URL de API**.

2. Inicie una sesión en {{site.data.keyword.cloud_notm}} con el siguiente mandato:
  ```
  cf login
  ```
  {: codeblock}

## Administración de usuarios
{: #admin_users}

### Adición de un usuario
{: #admin_add_user}

Para añadir un usuario al entorno de {{site.data.keyword.cloud_notm}} desde el registro de usuarios
para su entorno, utilice el mandato siguiente:
```
cf ba add-user user_name organization first_name last_name
```
{: codeblock}

Para añadir un usuario a una organización específica, debe ser un administrador con el permiso users.write (o Superusuario). Si es un gestor de organización, también se le puede proporcionar la posibilidad de añadir usuarios a su organización mediante un Superusuario que ejecute el mandato **`enable-managers-add-users`**. Para obtener más información, consulte [Permitir a los gestores agregar usuarios](#clius_emau).

<dl>
<dt>user_name</dt>
<dd>El nombre del usuario en el registro de LDAP.</dd>
<dt>organization</dt>
<dd>El nombre o GUID de la organización {{site.data.keyword.cloud_notm}} a la que se va a añadir el usuario.</dd>
<dt>first_name</dt>
<dd>El nombre del usuario que se añadirá a la organización.</dd>
<dt>last_name</dt>
<dd>El apellido del usuario que se añadirá a la organización.</dd>
</dl>

También puede usar **`ba au`** como alias para el nombre de mandato **`ba add-user`** más largo.
{: tip}

### Invitación a un usuario de {{site.data.keyword.Bluemix_dedicated_notm}}
{: #admin_dedicated_invite_public}

Cada entorno de {{site.data.keyword.Bluemix_dedicated_notm}} tiene una cuenta corporativa pública, propiedad del cliente, en {{site.data.keyword.cloud_notm}}. Para que los usuarios del entorno Dedicado creen clústeres con {{site.data.keyword.containershort}}, el administrador debe añadir a los usuarios a esta cuenta corporativa pública. Cuando se añaden usuarios a la cuenta corporativa pública, sus cuentas públicas y dedicadas quedan enlazadas. Los usuarios pueden utilizar su IBMid para iniciar sesión en ambas simultáneamente, y pueden crear recursos en la cuenta pública de la interfaz dedicada. Para obtener más información, consulte [Configuración de IBM Cloud Container Service en Dedicado](/docs/containers?topic=containers-dedicated#dedicated_setup). Para invitar a los usuarios dedicados a la cuenta pública:
```
cf ba invite-users-to-public -userid=user_email -organization=dedicated_org_id -apikey=public_api_key -public_org_id=public_org_id
```
{: pre}

Para añadir usuarios del entorno Dedicado a su cuenta pública de {{site.data.keyword.cloud_notm}}, debe ser un Administrador de la cuenta Dedicada.

<dl>
<dt>user_email</dt>
<dd>Si va a invitar a un único usuario, el correo electrónico del usuario.</dd>
<dt>dedicated_org_id</dt>
<dd>Si va a invitar invitando a todos los usuarios actuales de una organización de cuenta Dedicada, el ID de organización de cuenta Dedicada.</dd>
<dt>public_api_key</dt>
<dd>Una clave de API para invitar a usuarios a la cuenta pública. Debe generarla el administrador de la cuenta pública.</dd>
<dt>public_org_id</dt>
<dd>El ID de la organización de cuenta pública a la que va a invitar a los usuarios.</dd>
</dl>

### Listado de usuarios invitados desde {{site.data.keyword.Bluemix_dedicated_notm}}
{: #admin_dedicated_list}

Si invita a los usuarios del entorno Dedicado a su cuenta de {{site.data.keyword.cloud_notm}} con el [mandato **`invite-users-to-public`**](#admin_dedicated_invite_public), puede listar a los usuarios en su cuenta para ver el estado de su invitación. Los usuarios invitados con un IBMid existente tienen el estado ACTIVE. Los usuarios que no tengan un IBMid existente tienen el estado PENDING o ACTIVE, en función de si se ha aceptado la invitación. Para listar los usuarios de su cuenta de {{site.data.keyword.cloud_notm}}:

```
cf ba invite-users-status -apikey=public_api_key
```
{: pre}

Para añadir usuarios del entorno Dedicado a su cuenta pública de {{site.data.keyword.cloud_notm}}, debe ser un administrador de la cuenta Dedicada.

<dl>
<dt>public_api_key</dt>
<dd>La clave de API que se ha utilizado para invitar a los usuarios a la cuenta. Debe generarla el administrador de la cuenta pública.</dd>
</dl>

<!-- staging-only commands start. Live for interconnect -->

### Búsqueda de un usuario
{: #admin_search_user}

Para buscar un usuario, utilice el siguiente mandato junto con los parámetros de filtro de búsqueda opcionales (nombre, permiso, organización y rol):

```
cf ba search-users -name=user_name -permission=permission_value -organization=organization_value -role=role_value
```
{: codeblock}

<dl>
<dt>user_name</dt>
<dd>El nombre del usuario.</dd>
<dt>permission_value</dt>
<dd>El permiso asignado al usuario. Los permisos disponibles son admin (o superuser), log in (o basic), catalog.read, catalog.write, reports.read, reports.write, users.read o users.write. No se puede utilizar este parámetro con el parámetro de organización en la misma consulta.</dd>
<dt>organization_value</dt>
<dd>El nombre de la organización a la que pertenece el usuario. No se puede utilizar este parámetro con el parámetro de permiso en la misma consulta.</dd>
<dt>role_value</dt>
<dd>El rol de organización asignado al usuario. Los roles disponibles son auditors, managers y billing_managers. Especifique la organización con este parámetro.</dd>
</dl>

También puede usar **`ba su`** como alias para el nombre de mandato **`ba search-users`** más largo.
{: tip}

### Establecimiento de permisos para un usuario
{: #admin_setperm_user}

Puede establecer los permisos de uno en uno. Para establecer permisos para un usuario especificado, utilice el siguiente mandato:
```
cf ba set-permissions user_name permission access
```
{: codeblock}

<dl>
<dt>user_name</dt>
<dd>El nombre del usuario.</dd>
<dt>permission</dt>
<dd>Establece el permiso asignado al usuario. Los permisos disponibles son admin (o superuser), log in (o basic), catalog.read, catalog.write, reports.read, reports.write, users.read o users.write. No se puede utilizar este parámetro con el parámetro de organización en la misma consulta.</dd>
<dt>access</dt>
<dd>Para permisos del catálogo, informes o usuarios, también debe tener el nivel de acceso `read` o `write` (lectura o escritura).</dd>
</dl>

También puede usar **`ba sp`** como alias para el nombre de mandato **`ba set-permissions`** más largo.
{: tip}

<!-- staging-only commands end -->

### Eliminación de un usuario
{: #admin_remov_user}

Para eliminar un usuario del entorno de {{site.data.keyword.cloud_notm}}, utilice el siguiente mandato:

```
cf ba remove-user user_name
```
{: codeblock}

<dl>
<dt>user_name</dt>
<dd>El nombre del usuario en {{site.data.keyword.cloud_notm}}.</dd>
</dl>

También puede usar **`ba ru`** como alias para el nombre de mandato **`ba remove-user`** más largo.
{: tip}

### Permitir a los gestores agregar usuarios
{: #clius_emau}

Si tiene el permiso Superusuario en el entorno de {{site.data.keyword.cloud_notm}}, puede permitir a los gestores de la organización que agreguen usuarios a las organizaciones que gestionan. Para permitir a los gestores añadir usuarios, utilice el mandato siguiente:

```
cf ba enable-managers-add-users
```
{: codeblock}

También puede usar **`ba emau`** como alias para el nombre de mandato **`ba enable-managers-add-users`** más largo.
{: tip}

### No permitir a los gestores agregar usuarios
{: #clius_dmau}

Para no permitir a los gestores añadir usuarios, utilice el mandato siguiente:

```
cf ba disable-managers-add-users
```
{: codeblock}

También puede usar **`ba dmau`** como alias para el nombre de mandato **`ba disable-managers-add-users`** más largo.
{: tip}

## Administración de organizaciones
{: #admin_orgs}

### Adición de una organización
{: #admin_add_org}

Para añadir una organización, utilice el siguiente mandato:

```
cf ba create-org organization manager
```
{: codeblock}

<dl>
<dt>organization</dt>
<dd>El nombre o GUID de la organización de {{site.data.keyword.cloud_notm}} a añadir.</dd>
<dt>manager</dt>
<dd>El nombre de usuario del gestor de la organización.</dd>
</dl>

También puede usar **`ba co`** como alias para el nombre de mandato **`ba create-org`** más largo.
{: tip}

### Supresión de una organización
{: #admin_delete_org}

Para suprimir una organización, utilice el siguiente mandato:

```
cf ba delete-org organization
```
{: codeblock}

<dl>
<dt>organization</dt>
<dd>El nombre o GUID de la organización de {{site.data.keyword.cloud_notm}} que va a suprimir.</dd>
</dl>

También puede usar **`ba do`** como alias para el nombre de mandato **`ba delete-org`** más largo.
{: tip}

### Asignación de un usuario a una organización
{: #admin_ass_user_org}

Para asignar un usuario del entorno de {{site.data.keyword.cloud_notm}} a una
organización concreta, utilice el siguiente mandato:

```
cf ba set-org user_name organization [role]
```
{: codeblock}

<dl>
<dt>user_name</dt>
<dd>El nombre del usuario.</dd>
<dt>organization</dt>
<dd>El nombre o GUID de la organización {{site.data.keyword.cloud_notm}} a la que se va a asignar el usuario.</dd>
<dt>role</dt>
<dd>El rol del usuario. Los valores válidos son OrgManager, BillingManager, OrgAuditor. Consulte [Roles](/docs/iam?topic=iam-userroles#userroles) para ver las descripciones de los roles.</dd>
</dl>

También puede usar **`ba so`** como alias para el nombre de mandato **`ba set-org`** más largo.
{: tip}

### Eliminación de la asignación de un usuario de una organización
{: #admin_unass_user_org}

Para desasignar un usuario del entorno de {{site.data.keyword.cloud_notm}} desde una
organización concreta, utilice el siguiente mandato:

```
cf ba unset-org user_name organization [role]
```
{: codeblock}

<dl>
<dt>user_name</dt>
<dd>El nombre del usuario.</dd>
<dt>organization</dt>
<dd>El nombre o GUID de la organización de {{site.data.keyword.cloud_notm}}.</dd>
<dt>role</dt>
<dd>El rol del usuario. Los valores válidos son OrgManager, BillingManager, OrgAuditor. Consulte [Roles](/docs/iam?topic=iam-userroles#userroles) para ver las descripciones de los roles.</dd>
</dl>

También puede usar **`ba uo`** como alias para el nombre de mandato **`ba unset-org`** más largo.
{: tip}

### Configuración de una cuota para una organización
{: #admin_set_org_quota}

Para establecer la cuota de uso para una organización concreta, utilice el mandato siguiente:

```
cf ba set-quota organization plan
```
{: codeblock}

<dl>
<dt>organization</dt>
<dd>El nombre o GUID de la organización de {{site.data.keyword.cloud_notm}} para la que va a definir la cuota.</dd>
<dt>plan</dt>
<dd>El plan de cuotas de una organización.</dd>
</dl>

También puede usar **`ba sq`** como alias para el nombre de mandato **`ba set-quota`** más largo.
{: tip}


### Búsqueda de cuotas de contenedor para una organización
{: #admin_find_containquotas}

Para buscar la cuota de contenedores para una organización, utilice el siguiente mandato:

```
cf ibmcloud-admin containers-quota organization
```
{: codeblock}

<dl>
<dt>organization</dt>
<dd>El nombre o ID de la organización en IBM Cloud. Este
parámetro es obligatorio.</dd>
</dl>

También puede usar **`ba cq`** como alias para el nombre de mandato **`ibmcloud-admin containers-quota`** más largo.
{: tip}

### Configuración de cuotas de contenedor para una organización
{: #admin_set_containquotas}

Para definir la cuota de contenedores para una organización, utilice el siguiente mandato con al menos una de las opciones que se incluyen:

```
cf ibmcloud-admin set-containers-quota organization options
```
{: codeblock}

Puede incluir varias opciones, pero debe incluir al menos una.
{: note}

<dl>
<dt>organization</dt>
<dd>El nombre o ID de la organización de {{site.data.keyword.cloud_notm}} para la que va a definir la cuota.</dd>
<dt>options</dt>
<dd>Las opciones son: el valor floating-ips-max (abreviado fim), el valor memory-max (abreviado mm), el valor memory-space-default (abreviado msd), o el valor image-limit (abreviado il). El valor debe ser un entero.</dd>
</dl>

Opcionalmente, puede proporcionar un archivo que contenga parámetros de configuración específicos en un objeto JSON válido. Si utiliza la opción **`-file`**, esta prevalece y las otras opciones se pasan por alto. Para proporcionar un archivo en lugar de definir las opciones, utilice el siguiente mandato:

```
cf ibmcloud-admin set-containers-quota organization -file path_to_JSON_file
```
{: codeblock}

El archivo JSON debe tener el formato que se muestra en el siguiente ejemplo:

```
{
  "floating_ips_max": 10,
  "floating_ips_space_default": 0,
  "ram_max": 4096,
  "ram_space_default": 0,
  "image_limit": 10
}
```
{: codeblock}

También puede usar **`ba scq`** como alias para el nombre de mandato **`ibmcloud-admin set-containers-quota`** más largo.
{: tip}

## Administración de espacios
{: #admin_spaces}

### Añadir un espacio a la organización

Para añadir un espacio a la organización, utilice el mandato siguiente:

```
cf ibmcloud-admin create-space organization space_name
```

{: codeblock}

<dl>
<dt>organization</dt>
<dd>El nombre o GUID de la organización a la que se va a añadir el espacio.</dd>
<dt>space_name</dt>
<dd>El nombre del espacio que añade a la organización.</dd>
</dl>

También puede usar **`ba cs`** como alias para el nombre de mandato **`ba create-space`** más largo.
{: tip}

### Suprimir un espacio de la organización

Para eliminar un espacio de la organización, utilice el mandato siguiente:

```
cf ibmcloud-admin delete-space organization space_name
```

{: codeblock}

<dl>
<dt>organization</dt>
<dd>El nombre o GUID de la organización de la que se elimina el espacio.</dd>
<dt>space_name</dt>
<dd>El nombre del espacio que se elimina de la organización.</dd>
</dl>

También puede usar **`ba cs`** como alias para el nombre de mandato **`ba delete-space`** más largo.
{: tip}

### Añadir un usuario a un espacio con un rol

Para crear un usuario en un espacio con un rol específico, utilice el mandato siguiente:

```
cf ibmcloud-admin set-space organization space_name user_name role
```

{: codeblock}

<dl>
<dt>organization</dt>
<dd>El nombre o GUID de la organización a la que se añade el usuario.</dd>
<dt>space_name</dt>
<dd>El nombre del espacio al que se añade el usuario.</dd>
<dt>user_name</dt>
<dd>El nombre del usuario.</dd>
<dt>role</dt>
<dd>El rol del usuario. Los valores válidos son Manager, Developer o Auditor.</dd>
</dl>

También puede usar **`ba ss`** como alias para el nombre de mandato **`ba set-space`** más largo.
{: tip}


### Eliminar el rol de un usuario en un espacio

Para eliminar el rol de un usuario en un espacio, utilice el mandato siguiente:

```
cf ibmcloud-admin unset-space organization space_name user_name role
```

{: codeblock}

<dl>
<dt>organization</dt>
<dd>El nombre o GUID de la organización a la que pertenece el usuario.</dd>
<dt>space_name</dt>
<dd>El nombre del espacio al que pertenece el usuario.</dd>
<dt>user_name</dt>
<dd>El nombre del usuario.</dd>
<dt>role</dt>
<dd>El rol del usuario. Los valores válidos son Manager, Developer o Auditor.</dd>
</dl>

También puede usar **`ba us`** como alias para el nombre de mandato **`ba unset-space`** más largo.
{: tip}

## Administración del catálogo
{: #admin_catalog}

### Habilitación de servicios para todas las organizaciones
{: #admin_ena_service_org}

Para permitir que un servicio se muestre en el catálogo de {{site.data.keyword.cloud_notm}} para todas las organizaciones, utilice el siguiente mandato:

```
cf ba enable-service-plan plan_identifier
```
{: codeblock}

<dl>
<dt>plan_identifier</dt>
<dd>Nombre o GUID del plan de servicio que desea habilitar. Si especifica un nombre de plan de servicio no exclusivo, por ejemplo "Estándar" o "Básico", se le solicitará que seleccione un plan de servicio. Para identificar un nombre de plan, seleccione la categoría de servicio en la página de inicio y, a continuación, seleccione <b>Añadir</b> para ver los servicios para dicha categoría. Pulse el nombre de servicio para abrir la vista de detalles y luego podrá ver los nombres de los planes de servicio disponibles para dicho servicio. </dd>
</dl>

También puede usar **`ba esp`** como alias para el nombre de mandato **`ba enable-service-plan`** más largo.
{: tip}

### Inhabilitación de servicios para todas las organizaciones
{: #admin_dis_service_org}

Para no permitir que un servicio sea visible en el Catálogo de {{site.data.keyword.cloud_notm}} para todas las organizaciones, utilice el siguiente mandato:

```
cf ba disable-service-plan plan_identifier
```
{: codeblock}

<dl>
<dt>plan_identifier</dt>
<dd>Nombre o GUID del plan de servicio que desea habilitar. Si especifica un nombre de plan de servicio no exclusivo, por ejemplo "Estándar" o "Básico", se le solicitará que seleccione un plan de servicio. Para identificar un nombre de plan, seleccione la categoría de servicio en la página de inicio y, a continuación, seleccione <b>Añadir</b> para ver los servicios para dicha categoría. Pulse el nombre de servicio para abrir la vista de detalles y luego podrá ver los nombres de los planes de servicio disponibles para dicho servicio.</dd>
</dl>

También puede usar **`ba dsp`** como alias para el nombre de mandato **`ba disable-service-plan`** más largo.
{: tip}

### Adición de la visibilidad de los servicios de las organizaciones
{: #admin_addvis_service_org}

Puede añadir una organización de la lista de organizaciones que pueden ver un servicio específico en el Catálogo de {{site.data.keyword.cloud_notm}}. Para permitir que una organización pueda ver un servicio específico en el catálogo, utilice el mandato siguiente:

```
cf ba add-service-plan-visibility plan_identifier organization
```
{: codeblock}

<dl>
<dt>plan_identifier</dt>
<dd>Nombre o GUID del plan de servicio que desea habilitar. Si especifica un nombre de plan de servicio no exclusivo, por ejemplo "Estándar" o "Básico", se le solicitará que seleccione un plan de servicio. Para identificar un nombre de plan, seleccione la categoría de servicio en la página de inicio y, a continuación, seleccione <b>Añadir</b> para ver los servicios para dicha categoría. Pulse el nombre de servicio para abrir la vista de detalles y luego podrá ver los nombres de los planes de servicio disponibles para dicho servicio.</dd>
<dt>organization</dt>
<dd>El nombre o GUID de la organización de que va a añadir a la lista de visibilidad del servicio.</dd>
</dl>

También puede usar **`ba aspv`** como alias para el nombre de mandato **`ba add-service-plan-visibility`** más largo.
{: tip}

### Eliminación de la visibilidad de los servicios de las organizaciones
{: #admin_remvis_service_org}

Puede eliminar una organización de la lista de organizaciones que pueden ver un servicio específico en el Catálogo de {{site.data.keyword.cloud_notm}}. Para eliminar la visibilidad de un servicio en el catálogo de una organización, utilice el mandato siguiente:

```
cf ba remove-service-plan-visibility plan_identifier organization
```
{: codeblock}

<dl>
<dt>plan_identifier</dt>
<dd>Nombre o GUID del plan de servicio que desea habilitar. Si especifica un nombre de plan de servicio no exclusivo, por ejemplo "Estándar" o "Básico", se le solicitará que seleccione un plan de servicio. Para identificar un nombre de plan, seleccione la categoría de servicio en la página de inicio y, a continuación, seleccione <b>Añadir</b> para ver los servicios para dicha categoría. Pulse el nombre de servicio para abrir la vista de detalles y luego podrá ver los nombres de los planes de servicio disponibles para dicho servicio.</dd>
<dt>organization</dt>
<dd>El nombre o GUID de la organización que va a eliminar de la lista de visibilidad del servicio.</dd>
</dl>

También puede usar **`ba rspv`** como alias para el nombre de mandato **`ba remove-service-plan-visibility`** más largo.
{: tip}

### Edición de la visibilidad de los servicios de las organizaciones
{: #admin_editvis_service_org}

Puede editar y sustituir la lista de servicios que pueden ver determinadas organizaciones en el Catálogo de {{site.data.keyword.cloud_notm}}. Para sustituir todos los servicios visibles existentes de una o varias organizaciones, utilice el mandato siguiente:

```
cf ba edit-service-plan-visibilities plan_identifier organization_1 optional_organization_2
```
{: codeblock}

Este mandato sustituye los servicios visibles existentes de las organizaciones especificadas por el servicio que especifique en el mandato.

<dl>
<dt>plan_identifier</dt>
<dd>Nombre o GUID del plan de servicio que desea habilitar. Si especifica un nombre de plan de servicio no exclusivo, por ejemplo "Estándar" o "Básico", se le solicitará que seleccione un plan de servicio. Para identificar un nombre de plan, seleccione la categoría de servicio en la página de inicio y, a continuación, seleccione <b>Añadir</b> para ver los servicios para dicha categoría. Pulse el nombre de servicio para abrir la vista de detalles y luego podrá ver los nombres de los planes de servicio disponibles para dicho servicio.</dd>
<dt>organization</dt>
<dd>El nombre o GUID de la organización a la que va a añadir visibilidad. Puede habilitar la visibilidad del servicio a más de una organización especificando nombres o GUID adicionales en el mandato.</dd>
</dl>

También puede usar **`ba espv`** como alias para el nombre de mandato **`ba edit-service-plan-visibility`** más largo.
{: tip}

## Administración de informes
{: #admin_add_report}

### Adición de informes
{: #admin_adding_report}

Para añadir un informe de seguridad, utilice el siguiente mandato:

```
cf ba add-report category date PDF|TXT|LOG RTF
```
{: codeblock}

Si tiene acceso de escritura para el permiso de informes, puede crear una nueva categoría y añadir un informe en cualquiera de los formatos aceptados para sus usuarios. Especifique el nombre de la nueva categoría para el parámetro **`category`** o añada su informe en una categoría existente.

<dl>
<dt>category</dt>
<dd>La categoría del informe. Utilice las comillas si hay un espacio en el nombre.</dd>
<dt>date</dt>
<dd>La fecha del informe con el formato AAAAMMDD.</dd>
<dt>PDF|TXT|LOG</dt>
<dd>La vía de acceso del PDF del informe, del archivo de texto o de registro que va a cargar.</dd>
<dt>RTF</dt>
<dd>Opción para incluir una versión de formato de texto enriquecido (RTF) del PDF. Esta opción solo se aplica si incluye una vía de acceso al PDF del informe. La versión RTF se utiliza para indexar y buscar.</dd>
</dl>

También puede usar **`ba ar`** como alias para el nombre de mandato **`ba add-report`** más largo.
{: tip}

### Supresión de informes
{: #admin_del_report}

Para suprimir un informe de seguridad, utilice el siguiente mandato:

```
cf ba delete-report category date name
```
{: codeblock}

<dl>
<dt>category</dt>
<dd>La categoría del informe. Utilice las comillas si hay un espacio en el nombre.</dd>
<dt>date</dt>
<dd>La fecha del informe con el formato AAAAMMDD.</dd>
<dt>name</dt>
<dd>El nombre del informe.</dd>
</dl>

También puede usar **`ba dr`** como alias para el nombre de mandato **`ba delete-report`** más largo.
{: tip}

### Recuperación de informes
{: #admin_retr_report}

Para recuperar un informe de seguridad, utilice el siguiente mandato:

```
cf ba retrieve-report search
```
{: codeblock}

<dl>
<dt>search</dt>
<dd>El nombre de archivo del informe. Utilice las comillas si hay un espacio en el nombre.</dd>
</dl>

También puede usar **`ba rr`** como alias para el nombre de mandato **`ba retrieve-report`** más largo.
{: tip}

## Visualización de información de métricas de recursos
{: #cliresourceusage}

Puede ver información sobre métricas de recursos, incluidos el uso de memoria, de disco y de CPU. Puede ver un resumen de los recursos reservados y físicos disponibles y el uso de los recursos reservados y físicos. También puede ver los datos de uso de DEA (Droplet Execution Agent) y de las células (arquitectura de Diego). Para ver la información de métricas de recursos, utilice el mandato siguiente:

```
cf ba resource-metrics
```

También puede usar **`ba rsm`** como alias para el nombre de mandato **`ba resource-metrics`** más largo.
{: tip}

## Visualización del historial de métricas de recursos
{: #cliresourceusagehistory}

Puede recuperar el historial de métricas de recursos para el uso de disco y de memoria. Las métricas devueltas incluyen la cantidad de recursos que se utilizan del total disponible, para recursos tanto físicos como reservados. Los datos históricos del uso de memoria y de disco pueden mostrarse por hora, por día o por mes. Puede especificar las fechas de inicio y de finalización para recuperar datos dentro de un intervalo de fechas específico. Si no se especifica ninguna fecha, los datos históricos predeterminados son los datos de memoria por hora de las últimas 48 horas. Los datos se muestran en orden descendentes, mostrando primero las fechas más recientes. Para ver la información de historial de métricas de recursos, utilice el mandato siguiente:

```
cf ba resource-metrics-history hourly|daily|monthly  memory|disk   start|end
```
{: codeblock}

<dl>
<dt>--hourly</dt>
<dd>Ver los datos históricos de las últimas 48 horas. Éste es el valor predeterminado.</dd>
<dt>--daily</dt>
<dd>Ver el promedio diario de los datos históricos de los últimos 30 días.</dd>
<dt>--monthly</dt>
<dd>Ver el promedio mensual de los datos históricos de los últimos 6 meses.</dd>
<dt>--memory</dt>
<dd>Ver la memoria física y reservada utilizada y total.</dd>
<dt>--disk</dt>
<dd>Ver el disco físico y reservado utilizado y total.</dd>
<dt>--start</dt>
<dd>Especificar una fecha de inicio para daily o monthly con el formato mm-dd-aaaa, o una fecha y hora de inicio para hourly con el formato mm-dd-aaaa hh:mm:ss huso horario.</dd>
<dt>--end</dt>
<dd>Especificar una fecha de finalización para daily o monthly con el formato mm-dd-aaaa, o una fecha y hora de finalización para hourly con el formato mm-dd-aaaa hh:mm:ss huso horario.</dd>
</dl>

### Ejemplos
{: #cliresourceusagehistoryex}

```
cf ibmcloud-admin resource-metrics-history
cf ibmcloud-admin resource-metrics-history --daily --disk --start=07-04-2017
cf ibmcloud-admin resource-metrics-history --monthly --memory
cf ibmcloud-admin resource-metrics-history --hourly --start="06-01-2017 00:00:00 EDT" --end="06-30-2017 23:59:00 EDT
```
{: codeblock}

Puede visualizar la lista anterior de parámetros de mandatos y ejemplos utilizando el mandato siguiente:

```
cf ba resource-metrics-history -help
```

También puede usar **`ba rsmh`** como alias para el nombre de mandato **`ba resource-metrics-history`** más largo.
{: tip}

## Administración de intermediarios de servicio
{: #admin_servbro}

### Listado de intermediarios de servicio
{: #clilistservbro}

Para listar los intermediarios de servicio, utilice el mandato siguiente:

```
cf ba service-brokers broker_name
```
{: codeblock}

Para mostrar una lista de todos los intermediarios de servicio, especifique el mandato sin el parámetro
**`broker_name`**.

<dl>
<dt>broker_name</dt>
<dd>El nombre del intermediario de servicio personalizado. Utilice este parámetro, si quiere obtener información
para un intermediario de servicio específico. Opcional.</dd>
</dl>

También puede usar **`ba sb`** como alias para el nombre de mandato **`ba service-brokers`** más largo.
{: tip}

### Adición de un intermediario de servicio
{: #cliaddservbro}

Para añadir un intermediario de servicio, de modo que pueda añadir un servicio personalizado al catálogo de {{site.data.keyword.cloud_notm}}, utilice el mandato siguiente:

```
cf ba add-service-broker broker_name user_name password broker_url
```
{: codeblock}

<dl>
<dt>broker_name</dt>
<dd>El nombre del intermediario de servicio personalizado.</dd>
<dt>user_name</dt>
<dd>El nombre de usuario de la cuenta que tiene acceso al intermediario de servicios.</dd>
<dt>password</dt>
<dd>La contraseña de la cuenta que tiene acceso al intermediario de servicios.</dd>
<dt>broker_url</dt>
<dd>El URL del intermediario de servicio.</dd>
</dl>

También puede usar **`ba asb`** como alias para el nombre de mandato **`ba add-service-broker`** más largo.
{: tip}

### Supresión de un intermediario de servicio
{: #clidelservbro}

Para suprimir un intermediario de servicio que elimine el servicio personalizado del catálogo de {{site.data.keyword.cloud_notm}}, utilice el mandato siguiente:

```
cf ba delete-service-broker service_broker
```
{: codeblock}

<dl>
<dt>service_broker</dt>
<dd>El nombre o GUID del intermediario de servicio personalizado.</dd>
</dl>

También puede usar **`ba dsb`** como alias para el nombre de mandato **`ba delete-service-broker`** más largo.
{: tip}

### Actualización de un intermediario de servicio
{: #cliupdservbro}

Para actualizar un intermediario de servicio, utilice el mandato siguiente:

```
cf ba update-service-broker broker_name user_name password broker_url
```
{: codeblock}

<dl>
<dt>broker_name</dt>
<dd>El nombre del intermediario de servicio personalizado.</dd>
<dt>user_name</dt>
<dd>El nombre de usuario de la cuenta que tiene acceso al intermediario de servicios.</dd>
<dt>password</dt>
<dd>La contraseña de la cuenta que tiene acceso al intermediario de servicios.</dd>
<dt>broker_url</dt>
<dd>El URL del intermediario de servicio.</dd>
</dl>

También puede usar **`ba usb`** como alias para el nombre de mandato **`ba update-service-broker`** más largo.
{: tip}

## Administración de grupos de seguridad de aplicaciones
{: #admin_secgro}

Para trabajar con grupos de seguridad de aplicaciones (ASG), debe ser un administrador con acceso completo al entorno local o dedicado. Todos los usuarios del entorno pueden mostrar una lista de los ASG disponibles para la organización que el mandato tiene como objetivo. No obstante, para crear, actualizar o enlazar ASG, debe ser administrador del entorno de {{site.data.keyword.cloud_notm}}.

Los ASG funcionan como cortafuegos virtuales que controlan el tráfico de salida de las apps del entorno de
{{site.data.keyword.cloud_notm}}. Cada ASG está compuesto por una lista de reglas que permiten comunicaciones y tráfico específicos hacia y desde el exterior de la red. Puede enlazar uno o más ASG con un conjunto de grupos de seguridad específico. Por ejemplo, si aplica acceso global para un conjunto de grupos o enlaza espacios dentro de una organización en el entorno de {{site.data.keyword.cloud_notm}}.

{{site.data.keyword.cloud_notm}} se configura inicialmente con todo el acceso a la red externa restringido. Dos grupos de seguridad creados por IBM, `public_networks` y `dns`, permiten el acceso global a la red externa al enlazar dichos grupos con los conjuntos de grupos de seguridad de Cloud Foundry predeterminados. Los dos conjuntos de grupos de seguridad de Cloud Foundry que se utilizan para aplicar el acceso global son los conjuntos de grupos **Default Staging** y **Default Running**. Estos conjuntos de grupos aplican las reglas para permitir tráfico hacia todas las apps en ejecución o todas las apps en transferencia. Si no desea enlazar estos dos conjuntos de grupos de seguridad, puede desenlazarlos de los conjuntos de grupos de Cloud Foundry y, a continuación, enlazar el grupo de seguridad con un espacio específico. Para obtener más información, consulte
[Enlace de grupos de seguridad de aplicaciones](https://docs.cloudfoundry.org/concepts/asg.html#binding-groups){: new_window} ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo").

Al desenlazar los conjuntos de grupos **Default Staging** o **Default Running** de los dos grupos de seguridad creados por IBM, `public_networks` y `dns` inhabilitarán el acceso global a la red externa. Utilice la acción de desenlazar con precaución y conocimiento de su efecto potencial en las apps en ejecución y en transferencia de su entorno.
{: important}

Los mandatos siguientes que le permiten trabajar con grupos de seguridad se basan en la versión 1.6 de Cloud Foundry. Para obtener más información, incluidos los campos necesarios y opcionales, consulte la información de Cloud Foundry acerca de la
[Creación de grupos de seguridad de aplicaciones](https://docs.cloudfoundry.org/concepts/asg.html#creating-groups){: new_window} ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo").

### Listado de grupos de seguridad
{: #clilissecgro}

Para listar todos los grupos de seguridad, utilice el siguiente mandato:

```
cf ba security-groups
```
{: codeblock}

Para mostrar detalles para un grupo de seguridad específico, utilice el mandato siguiente:

```
cf ba security-groups security-group
```
{: codeblock}

<dl>
<dt>Grupo de seguridad</dt>
<dd>El nombre del grupo de seguridad.</dd>
</dl>

También puede usar **`ba sg`** como alias para el nombre de mandato **`ba security-groups`** más largo.
{: tip}

### Creación de un grupo de seguridad
{: #clicreasecgro}

Para crear un grupo de seguridad, utilice el siguiente mandato:
```
cf ba create-security-group security-group path-to-rules-file
```
{: codeblock}

Cada grupo de seguridad que cree tiene el prefijo
`adminconsole_` añadido al nombre para distinguirlo de los grupos de seguridad creados por IBM.

<dl>
<dt>security-group</dt>
<dd>El nombre del grupo de seguridad.</dd>
<dt>path-to-rules-file</dt>
<dd>La vía de acceso absoluta o relativa al archivo de reglas.</dd>
</dl>

También puede usar **`ba csg`** como alias para el nombre de mandato **`ba create-security-group`** más largo.
{: tip}

Para obtener más información sobre la creación de grupos de seguridad y de las reglas que definen el tráfico de salida, consulte
[Creación de grupos de seguridad de aplicaciones](https://docs.cloudfoundry.org/concepts/asg.html#creating-groups){: new_window} ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo").

### Actualización de un grupo de seguridad
{: #cliupdsecgro}

Para actualizar un grupo de seguridad, utilice el siguiente mandato:

```
cf ba update-security-group security-group path-to-rules-file
```
{: codeblock}

<dl>
<dt>security-group</dt>
<dd>El nombre del grupo de seguridad.</dd>
<dt>path-to-rules-file</dt>
<dd>La vía de acceso absoluta o relativa al archivo de reglas.</dd>
</dl>

También puede usar **`ba usg`** como alias para el nombre de mandato **`ba update-security-group`** más largo.
{: tip}

### Supresión de un grupo de seguridad
{: #clidelsecgro}

Para suprimir un grupo de seguridad, utilice el siguiente mandato:
```
cf ba delete-security-group security-group
```
{: codeblock}

<dl>
<dt>Grupo de seguridad</dt>
<dd>Nombre del grupo de seguridad</dd>
</dl>

También puede usar **`ba dsg`** como alias para el nombre de mandato **`ba delete-security-group`** más largo.
{: tip}

### Enlace de grupos de seguridad
{: #clibindsecgro}

Para enlazar con el conjunto de grupos de seguridad Default Staging, utilice el siguiente mandato:

```
cf ba bind-staging-security-group security-group
```
{: codeblock}

<dl>
<dt>Grupo de seguridad</dt>
<dd>Nombre del grupo de seguridad</dd>
</dl>

También puede usar **`ba bssg`** como alias para el nombre de mandato **`ba bind-staging-security-group`** más largo.
{: tip}

Para enlazar con el conjunto de grupos de seguridad Default Running, utilice el siguiente mandato:

```
cf ba bind-running-security-group security-group
```
{: codeblock}

<dl>
<dt>Grupo de seguridad</dt>
<dd class="pd">Nombre del grupo de seguridad</dd>
</dl>

También puede usar **`ba brsg`** como alias para el nombre de mandato **`ba bind-running-security-group`** más largo.
{: tip}

Para enlazar un grupo de seguridad con un espacio, utilice el siguiente mandato:

```
cf ba bind-security-group security-group org space
```
{: codeblock}

<dl>
<dt>security-group</dt>
<dd>El nombre del grupo de seguridad.</dd>
<dt>org</dt>
<dd>El nombre de la organización con la que enlazar el grupo de seguridad.</dd>
<dt>espacio</dt>
<dd>El nombre del espacio dentro de la organización con el que enlazar el grupo de seguridad.</dd>
</dl>

También puede usar **`ba bsg`** como alias para el nombre de mandato **`ba bind-security-group`** más largo.
{: tip}

Para obtener más información sobre el enlace de grupos de seguridad, consulte
[Enlace de grupos de seguridad de aplicaciones](https://docs.cloudfoundry.org/concepts/asg.html#binding-groups){: new_window} ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo").

### Anulación de enlace de grupos de seguridad
{: #cliunbindsecgro}

Al desenlazar el conjunto de grupos Default Staging de los dos grupos de seguridad creados por IBM, `public_networks` y `dns`, se inhabilita el acceso global a la red externa y debe utilizarse con precaución y conocimiento de las ramificaciones que tiene en todas las apps en transferencia de su entorno. Para anular el enlace desde un conjunto de grupos de seguridad Default Staging, utilice el siguiente mandato:

```
cf ba unbind-staging-security-group security-group
```
{: codeblock}

<dl>
<dt>Grupo de seguridad</dt>
<dd>El nombre del grupo de seguridad.</dd>
</dl>

También puede usar **`ba ussg`** como alias para el nombre de mandato **`ba unbind-staging-security-group`** más largo.
{: tip}

Al desenlazar el conjunto de grupos Default Running de los dos grupos de seguridad creados por IBM; `public_networks` y `dns`, se inhabilita el acceso global a la red externa y debe utilizarse con precaución y conocimiento de las ramificaciones que tiene en todas las apps en ejecución de su entorno. Para anular el enlace desde un conjunto de grupos de seguridad Default Running, utilice el siguiente mandato:

```
cf ba unbind-running-security-group security-group
```
{: codeblock}

<dl>
<dt>Grupo de seguridad</dt>
<dd>El nombre del grupo de seguridad.</dd>
</dl>

También puede usar **`ba brsg`** como alias para el nombre de mandato **`ba unbind-running-security-group`** más largo.
{: tip}

Para anular el enlace de un grupo de seguridad con un espacio, utilice el siguiente mandato:

```
cf ba unbind-security-group security-group org space
```
{: codeblock}

<dl>
<dt>security-group</dt>
<dd>El nombre del grupo de seguridad.</dd>
<dt>org</dt>
<dd>El nombre de la organización de la que desenlazar el grupo de seguridad.</dd>
<dt>espacio</dt>
<dd>El nombre del espacio dentro de la organización del que desea desenlazar el grupo de seguridad.</dd>
</dl>

También puede usar **`ba usg`** como alias para el nombre de mandato **`ba unbind-security-group`** más largo.
{: tip}

Para obtener más información sobre cómo anular el enlace de grupos de seguridad, consulte
[Anulación del enlace de grupos de seguridad de aplicaciones](https://docs.cloudfoundry.org/concepts/asg.html#unbinding-groups){: new_window} ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo").

## Administración de paquetes de compilación
{: #admin_buildpack}

### Listado de paquetes de compilación
{: #clilistbuildpack}

Si tiene permisos de escritura en el catálogo de las apps, puede listar los paquetes de compilación. Para listar todos los paquetes de compilación o para ver un paquete de compilación específico, utilice el siguiente mandato:

```
cf ba buildpacks buildpack_name
```
{: codeblock}

<dl>
<dt>buildpack_name</dt>
<dd>Un parámetro opcional para especificar un paquete de compilación concreto para ver.</dd>
</dl>

También puede usar **`ba lb`** como alias para el nombre de mandato **`ba buildpacks`** más largo.
{: tip}

### Creación y carga de un paquete de compilación
{: #clicreupbuildpack}

Si tiene permisos de escritura en el catálogo de las apps, puede crear y cargar un paquete de compilación. Puede cargar cualquier archivo comprimido que tenga un tipo de archivo `.zip`. Para cargar un paquete de compilación, utilice el siguiente mandato:

```
cf ba create-buildpack buildpack_name file_path position
```
{: codeblock}

<dl>
<dt>buildpack_name</dt>
<dd>Nombre del paquete de compilación que se cargará.</dd>
<dt>file_path</dt>
<dd>Vía de acceso al archivo comprimido del paquete de compilación.</dd>
<dt>position</dt>
<dd>Orden en el que se comprueban los paquetes de compilación durante la detección automática del paquete de compilación.</dd>
</dl>

También puede usar **`ba cb`** como alias para el nombre de mandato **`ba create-buildpack`** más largo.
{: tip}

### Actualización de un paquete de compilación
{: #cliupdabuildpack}

Si tiene permisos de escritura en el catálogo de las apps, puede actualizar un paquete de compilación existente. Para actualizar un paquete de compilación, utilice el siguiente mandato:
```
cf ba update-buildpack buildpack_name position enabled locked
```
{: codeblock}

<dl>
<dt>buildpack_name</dt>
<dd>Nombre del paquete de compilación que se actualizará.</dd>
<dt>position</dt>
<dd>Orden en el que se comprueban los paquetes de compilación durante la detección automática del paquete de compilación.</dd>
<dt>enabled</dt>
<dd>Indica si el paquete de compilación se utilizará para la transferencia.</dd>
<dt>locked</dt>
<dd>Indica si el paquete de compilación está bloqueado para impedir actualizaciones.</dd>
</dl>

También puede usar **`ba ub`** como alias para el nombre de mandato **`ba update-buildpack`** más largo.
{: tip}

### Supresión de un paquete de compilación
{: #clidelbuildpack}

Si tiene permisos de escritura en el catálogo de las apps, puede suprimir un paquete de compilación existente. Para suprimir un paquete de compilación, utilice el siguiente mandato:
```
cf ba delete-buildpack buildpack_name
```
{: codeblock}

<dl>
<dt>buildpack_name</dt>
<dd>Nombre del paquete de compilación que se suprimirá.</dd>
</dl>

También puede usar **`ba db`** como alias para el nombre de mandato **`ba delete-buildpack`** más largo.
{: tip}