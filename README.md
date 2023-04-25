# Cibergestión seguros

## Servidor de procesos background

_Herramientas_

* [.NET 6](https://dotnet.microsoft.com/download/dotnet/6.0) - Framework
* [Hangfire](https://www.hangfire.io/) - Procesamiento background
* SQL Server

## Ejecutar
```sh
> dotnet restore
````

## User Secret
Comandos básicos de user-secrets
```sh
> dotnet user-secrets init                      -> Inicializa user-secrets
> dotnet user-secrets list						-> Lista todos los user-secrets
> dotnet user-secrets clear						-> Borra todos los user-secrets
> dotnet user-secrets remove "[KEY_A_REMOVER]"	-> Remueve user-secret especifico
```

Agregar user-secrets de proyecto BACKGROUND JOBS
```sh
> dotnet user-secrets init
> dotnet user-secrets set "ConnectionStrings:Marsh492Connection" "Data Source=[ServerNameOrIpServer];Initial Catalog=marsh_dev;User ID=[UserDB];Password=[PasswordUserDb];"
> dotnet user-secrets set "ConnectionStrings:HangfireConnection" "Data Source=[ServerNameOrIpServer];Initial Catalog=marsh_background_jobs;User ID=[UserDB];Password=[PasswordUserDb];"
> dotnet user-secrets set "EmailConfiguration:TemplateFolder" "[RUTA_PARA_PLANTILLAS_CORREOS]" 
> dotnet user-secrets set "DocumentConfiguration:TemplateFolder" "[RUTA_PARA_PLANTILLAS_REPORTES]" 
> dotnet user-secrets set "DocumentConfiguration:RepositoryFolder" "[RUTA_PARA_REPOSITORIO_DE_ARCHIVOS]"
```

## Para VS añadirlos en sus user secrets sin el > y cambiar sus credenciales en las cadenas de conexion
```sh
>  "EmailConfiguration:TemplateFolder": "C:\\Repository\\Marsh\\Email\\Templates",
>  "DocumentConfiguration:TemplateFolder": "C:\\Repository\\Marsh\\Document\\Templates",
>  "ConnectionStrings:HangfireConnection": "Data Source=localhost;Initial Catalog=marsh_background_jobs;User ID=sa;Password=12345;",
>  "ConnectionStrings:Marsh492Connection": "Data Source=localhost;Initial Catalog=marsh_dev;User ID=sa;Password=12345;",
>  "DocumentConfiguration:RepositoryFolder": "C:\\Repository\\Marsh\\Files"
```

## Crear base de datos
```sh
CREATE DATABASE marsh_492_background_jobs
GO
```

## Opcional
```sh
> dotnet new tool-manifest
> dotnet tool install Cake.Tool --version 1.1.0
```

## Configuración de correo electrónico
```sh
> dotnet user-secrets set "EmailConfiguration:From" "[MI_CORREO_PERSONAL]"
> dotnet user-secrets set "EmailConfiguration:User_Name" "[MI_CORREO_PERSONAL]"
> dotnet user-secrets set "EmailConfiguration:Password" "[MI_CONTRASENA_DE_APLICACIONES_GENERADA]"
```

## Generar 'Contraseña de Aplicaciones'
1. Abre tu correo corporativo y dirígete a la opción `Gestionar tu cuenta de Google`.
2. En la página de configuración de tu cuenta, utiliza el buscador para encontrar el módulo de `Contraseñas de aplicaciones`.
3. Al acceder al módulo, elige la opción `Seleccionar aplicación` y luego selecciona `Otra` para crear una contraseña personalizada.
4. Escribe un nombre para la aplicación, por ejemplo, `Marsh`.
5. Presiona el botón `Generar` para crear una nueva contraseña segura.
6. Copia la contraseña y pégala en tus **user-secrets** sección `EmailConfiguration:Password`.

> **Nota**: Si no se requiere el uso de `Contraseñas de Aplicación`, es necesario activar la opción `Acceso de aplicaciones menos seguras` en la sección de `Seguridad` de la cuenta.


