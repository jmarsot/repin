### ACCIONA REPO
Repositorio de Acciona

#### Terraform

Antes de lanzar los scripts de Terraform, desde powershell:

    az login

    az account set --subscription="SUBSCRIPTION_ID"

    az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/SUBSCRIPTION_ID"

Scripts totalmente parametrizados.

Para ver los cambios que se van a aplicar:

    terraform plan -var-file="development.tfvars"
    terraform plan -var-file="production.tfvars"

Para crear la infra después del plan:

    terraform apply -var-file="development.tfvars"
    terraform apply -var-file="production.tfvars"


### Pasos a dar desde la interfaz:

 Una vez que se ha lanzado el script por primera vez, accederemos al workspace de Databricks, y en la opción de Account (icono de persona en la parte superior derecha), accederemos a la sección de "User settings", y ahí generaremos un Personal Access Token.
 El valor del access token que hemos generado lo almacenaremos como secret en nuestro Key Vault. Para ello, primero en archivo de variables.tf descomentaremos la variable "databricks_secret_value", después en el script "main.tf" descomentaremos bloque  "azurerm_key_vault_secret". Una vez hecho esto, volveremos a hacer un "Apply" en terraform y por consola nos pedirá introducir el valor de la variable "databricks_secret_value", y aquí meteremos el valor del access token de Databricks.

Para generar el recurso Data Catalog, desde la interfaz accederemos a la opción "Crear un recurso", desde ahí buscaremos por "Data Catalog", y le daremos al botón de "Crear". Tendremos que indicar las opciones de:
Suscripción, Grupo de Recursos, un nombre para el Data Catalog, la ubicación y el rango de precio. 

Para generar el recurso Machine Learning, desde la interfaz accederemos a la opción "Crear un recurso", desde ahí buscaremos por "Machine Learning", y le daremos al botón de "Crear". Ahí además de un nombre al recurso, tendremos que indicar el grupo de recursos específico creado de Machine Learning. 