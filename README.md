# Configuracion NetCore

## Documentacion

Proyecto NetCore
 - Core : Esta carpeta contendrá todas las clases entidades e interfaces del
project.
 - Infrastructure : esa carpeta va a contener todo lo relacionado con el acceso de
datos, los repositorios y las unidades de trabajo.
 - Api: esta carpeta guardará el proyecto donde crearemos las diferentes apis o
Endpoints para ser consumidos por las aplicaciones externas.



**Comandos utilizados para la creacion de mi proyecto (La estructura o Base del proyecto)**

```Terminal
1. dotnet tool install --global dotnet-ef                                                               ---> instala la herramienta "dotnet-ef" globalmente para trabajar con Entity Framework Core.

2. dotnet tool list -g                                                                                  ---> Lista las herramientas globales instaladas en .NET.

3. dotnet new sln                                                                                       ---> Crea una nueva solución de .NET.
---(Una solución (.sln) se refiere a un archivo que actúa como un contenedor para organizar y administrar proyectos relacionados en un entorno de desarrollo de .NET)


4. dotnet new webapi -o API                                                                             ---> Crea un nuevo proyecto de API web en la carpeta "API".

5. dotnet sln add API/                                                                                  ---> Agrega el proyecto "API" a la solución.

6. dotnet new classlib -o Core                                                                          ---> Crea un nuevo proyecto de biblioteca de clases en la carpeta "Core".

7. dotnet new classlib -o Infrastructure                                                                ---> Crea un nuevo proyecto de biblioteca de clases en la carpeta "Infrastructure".

8. dotnet sln add Core/                                                                                 ---> Agrega el proyecto "Core" a la solución.

9. dotnet sln add Infrastructure/                                                                       ---> Agrega el proyecto "Infrastructure" a la solución.


10. cd Infrastructure/
    - dotnet add reference ../Core/                                                                     ---> Agrega una referencia al proyecto "Core" desde el proyecto "Infrastructure".


12. cd API/
    - dotnet add reference ../Infrastructure/                                                           ---> Agrega una referencia al proyecto "Infrastructure" desde el proyecto "API".


13. cd Infrastructure/
    - dotnet add package Microsoft.EntityFrameworkCore --version 7.0.9                                  ---> Agrega el paquete de Entity Framework Core versión 7.0.9 al proyecto "Infrastructure".
    - dotnet add package Pomelo.EntityFrameworkCore.MySql --version 7.0.0                               ---> Agrega el paquete de Entity Framework Core para MySQL versión 7.0.0 al proyecto "Infrastructure".


14. cd API/
    - dotnet add package Microsoft.EntityFrameworkCore.Design --version 7.0.8                           ---> Agrega el paquete de diseño de Entity Framework Core versión 7.0.8 al proyecto "API".
    - dotnet add package AutoMapper.Extensions.Microsoft.DependencyInjection --version 12.0.1           ---> Se utiliza para agregar el paquete de AutoMapper.Extensions.Microsoft.DependencyInjection en su versión 12.0.1 a un proyecto de .NET.


**Como hacer migraciones**
////////////////////////////////////////////////////////////////////////////////////////////////
Paso 1: Instalar Entity Framework
Asegúrate de tener instalado Entity Framework en tu proyecto. Puedes instalarlo a través de NuGet Package Manager utilizando el siguiente comando en la Consola del Administrador de Paquetes:

//Codigo
        Install-Package EntityFramework


////////////////////////////////////////////////////////////////////////////////////////////////

Paso 2: Crear una clase que herede de DbContext
Crea una clase que herede de DbContext. Esta clase representa el contexto de la base de datos y se utilizará para interactuar con la base de datos y definir los DbSet para las entidades que deseas persistir.

//Codigo
        using System.Data.Entity;

        public class MiDbContext : DbContext
        {
            public DbSet<MiEntidad> MisEntidades { get; set; }

            // Otros DbSet para otras entidades, si las hay

            // Constructor para pasar la cadena de conexión a la clase base DbContext
            public MiDbContext() : base("NombreDeTuCadenaDeConexion")
            {
            }
        }


////////////////////////////////////////////////////////////////////////////////////////////////
Paso 3: Definir tu entidad
Crea una clase para representar la entidad que deseas persistir en la base de datos.

//Codigo
        public class MiEntidad
        {
            public int Id { get; set; }
            public string Nombre { get; set; }

            // Otros campos de la entidad, si los hay
        }

////////////////////////////////////////////////////////////////////////////////////////////////
Paso 4: Habilitar las migraciones
Para habilitar las migraciones, abre la Consola del Administrador de Paquetes y selecciona el proyecto que contiene tu clase de contexto (MiDbContext). Luego, ejecuta el siguiente comando:

//Codigo
Enable-Migrations


////////////////////////////////////////////////////////////////////////////////////////////////
Paso 5: Crear una nueva migración
Para crear una nueva migración, utiliza el siguiente comando en la Consola del Administrador de Paquetes:

//Codigo
Add-Migration NombreDeTuMigracion

////////////////////////////////////////////////////////////////////////////////////////////////
Esto creará una nueva clase de migración con el nombre que especificaste en la carpeta "Migrations" de tu proyecto. Esta clase contiene las operaciones necesarias para aplicar los cambios en la base de datos.
////////////////////////////////////////////////////////////////////////////////////////////////
Paso 6: Aplicar la migración
Finalmente, para aplicar la migración a la base de datos, ejecuta el siguiente comando:

//Codigo
Update-Database

///////////////////////////////////////////////////////////////////////////////////////////////
Esto aplicará todas las migraciones pendientes y actualizará la base de datos con los cambios definidos en las clases de migración.
```

---
>ESTO ES IMPORTANTE
> - **Migrations** (Se deben utilizar estos comandos para poder aplicar las migraciones y que los cambios se guarden en la base de datos)
>   - dotnet ef migrations add InitialCreate --project ./Infrastructure/ --startup-project ./API/ --output-dir ./Data/Migrations
>   - dotnet ef database update --project ./Infrastructure/ --startup-project ./API/
> - **Errores** (Ambos comandos se utilizan para construir (compilar) los proyectos "Infrastructure" y "API" en sus respectivos directorios y tambien los podemos utilizar para ver que posibles errores podemos tener.)
>   - dotnet build ./Infrastructure/
>   - dotnet build ./API/




