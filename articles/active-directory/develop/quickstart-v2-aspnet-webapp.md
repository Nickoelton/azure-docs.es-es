---
title: 'Inicio rápido: Incorporación del inicio de sesión con Microsoft a una aplicación web ASP.NET | Azure'
titleSuffix: Microsoft identity platform
description: En este inicio rápido, aprenda a implementar el inicio de sesión de Microsoft en una aplicación web de ASP.NET mediante OpenID Connect.
services: active-directory
author: jmprieur
manager: CelesteDG
ms.service: active-directory
ms.subservice: develop
ms.topic: quickstart
ms.workload: identity
ms.date: 09/25/2020
ms.author: jmprieur
ms.custom: devx-track-csharp, aaddev, identityplatformtop40, scenarios:getting-started, languages:ASP.NET, contperf-fy21q1
ms.openlocfilehash: 4a0f43d93e848ee98560811d921e6b1168f35828
ms.sourcegitcommit: 126ee1e8e8f2cb5dc35465b23d23a4e3f747949c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/10/2021
ms.locfileid: "100103811"
---
# <a name="quickstart-add-microsoft-identity-platform-sign-in-to-an-aspnet-web-app"></a>Inicio rápido: Adición del inicio de sesión de la plataforma de identidad de Microsoft a una aplicación web de ASP.NET

En este inicio rápido, descargará y ejecutará un código de ejemplo que muestra cómo una aplicación web de ASP.NET puede realizar el inicio de sesión de los usuarios desde cualquier organización de Azure Active Directory. 

Para ilustrar este tema, consulte el apartado en el que se explica el [funcionamiento del ejemplo](#how-the-sample-works).
> [!div renderon="docs"]
> ## <a name="prerequisites"></a>Requisitos previos
>
> * Una cuenta de Azure con una suscripción activa. [Cree una cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).
> * [Visual Studio 2019](https://visualstudio.microsoft.com/vs/)
> * [.NET Framework 4.7.2+](https://dotnet.microsoft.com/download/visual-studio-sdks)
>
> ## <a name="register-and-download-your-quickstart-app"></a>Registro y descarga de la aplicación de inicio rápido
> Tiene dos opciones para comenzar con la aplicación de inicio rápido:
> * [Rápido] [Opción 1: registrar y configurar de modo automático la aplicación y, a continuación, descargar el código de ejemplo](#option-1-register-and-auto-configure-your-app-and-then-download-your-code-sample)
> * [Manual] [Opción 2: registrar y configurar manualmente la aplicación y el código de ejemplo](#option-2-register-and-manually-configure-your-application-and-code-sample)
>
> ### <a name="option-1-register-and-auto-configure-your-app-and-then-download-your-code-sample"></a>Opción 1: registrar y configurar de modo automático la aplicación y, a continuación, descargar el código de ejemplo
>
> 1. Vaya a la experiencia de inicio rápido <a href="https://portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/applicationsListBlade/quickStartType/AspNetWebAppQuickstartPage/sourceType/docs" target="_blank">Azure Portal: Registros de aplicaciones</a>.
> 1. Escriba un nombre para la aplicación y seleccione **Registrar**.
> 1. Siga las instrucciones para descargar y configurar automáticamente la nueva aplicación en un solo clic.
>
> ### <a name="option-2-register-and-manually-configure-your-application-and-code-sample"></a>Opción 2: registrar y configurar manualmente la aplicación y el código de ejemplo
>
> #### <a name="step-1-register-your-application"></a>Paso 1: Registrar su aplicación
> Para registrar la aplicación y agregar la información de registro de la aplicación a la solución de forma manual, siga estos pasos:
>
> 1. Inicie sesión en <a href="https://portal.azure.com/" target="_blank">Azure Portal</a>.
> 1. Si tiene acceso a varios inquilinos, use el filtro **Directorio + suscripción** :::image type="icon" source="./media/common/portal-directory-subscription-filter.png" border="false"::: del menú superior para seleccionar el inquilino en el que desea registrar una aplicación.
> 1. Busque y seleccione **Azure Active Directory**.
> 1. En **Administrar**, seleccione **Registros de aplicaciones** >  y, luego, **Nuevo registro**.
> 1. Escriba el **Nombre** de la aplicación, por ejemplo `ASPNET-Quickstart`. Los usuarios de la aplicación pueden ver este nombre, el cual se puede cambiar más tarde.
> 1. En **URI de redirección**, agregue `https://localhost:44368/` y seleccione **Registrar**.
> 1. En **Administrar**, seleccione **Autenticación**.
> 1. En la sección **Implicit grant and hybrid flows** (Flujos de concesión implícita e híbridos), seleccione **Tokens de id.**
> 1. Seleccione **Guardar**.

> [!div class="sxs-lookup" renderon="portal"]
> #### <a name="step-1-configure-your-application-in-azure-portal"></a>Paso 1: Configuración de la aplicación en Azure Portal
> Para que el código de ejemplo de este inicio rápido funcione, agregue un **identificador URI de redirección** de `https://localhost:44368/`.

> > [!div renderon="portal" id="makechanges" class="nextstepaction"]
> > [Hacer este cambio por mí]()
>
> > [!div id="appconfigured" class="alert alert-info"]
> > ![Ya configurada](media/quickstart-v2-aspnet-webapp/green-check.png) La aplicación está configurada con este atributo

#### <a name="step-2-download-your-project"></a>Paso 2: Descarga del proyecto

> [!div renderon="docs"]
> [Descargue la solución de Visual Studio 2019](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip)

> [!div renderon="portal" class="sxs-lookup"]
> Ejecute el proyecto con Visual Studio 2019.
> [!div renderon="portal" id="autoupdate" class="sxs-lookup nextstepaction"]
> [Descargar el código de ejemplo](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip)

> [!div class="sxs-lookup" renderon="portal"]
> #### <a name="step-3-your-app-is-configured-and-ready-to-run"></a>Paso 3: La aplicación está configurada y lista para ejecutarse
> Hemos configurado el proyecto con los valores de las propiedades de su aplicación.

> [!div renderon="docs"]
> #### <a name="step-3-run-your-visual-studio-project"></a>Paso 3: Ejecución del proyecto de Visual Studio

1. Extraiga el archivo ZIP en la carpeta local más próxima a la carpeta raíz (por ejemplo, **C:\Azure-Samples**).
1. Abra la solución en Visual Studio (AppModelv2-WebApp-OpenIDConnect-DotNet.sln)
1. Según la versión de Visual Studio que use, es posible que necesite hacer clic con el botón derecho en el proyecto `AppModelv2-WebApp-OpenIDConnect-DotNet` y **Restaurar paquetes NuGet**.
1. Abra la Consola del Administrador de paquetes (Ver -> Otras ventanas -> Consola del Administrador de paquetes) y ejecute `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`.

> [!div renderon="docs"]
> 5. Edite **Web.config** y reemplace los parámetros `ClientId` y `Tenant` por:
>    ```xml
>    <add key="ClientId" value="Enter_the_Application_Id_here" />
>    <add key="Tenant" value="Enter_the_Tenant_Info_Here" />
>    ```
>    Donde:
> - `Enter_the_Application_Id_here`: es el identificador de aplicación de la aplicación que registró.
> - `Enter_the_Tenant_Info_Here`: es una de las opciones siguientes:
>   - Si la aplicación admite **Solo mi organización**, reemplace este valor por el de **Identificador de inquilino** o el de **Nombre de inquilino** (por ejemplo, contoso.onmicrosoft.com)
>   - Si la aplicación admite **Cuentas en cualquier directorio organizativo**, reemplace este valor por `organizations`
>   - Si la aplicación admite **Todos los usuarios de cuentas Microsoft**, reemplace este valor por `common`
>
> > [!TIP]
> > - Para buscar los valores de *Identificador de aplicación*, *Identificador de directorio (inquilino)* y *Tipos de cuenta admitidos*, vaya a la página **Información general**
> > - Asegúrese de que el valor de `redirectUri` en **Web.config** se corresponde con el **URI de redirección** definido para el registro de la aplicación en Azure AD (si no es así, vaya al menú **Autenticación** para encontrar el registro de la aplicación y actualice el **URI DE REDIRECCIÓN** para que coincida)

> [!div class="sxs-lookup" renderon="portal"]
> > [!NOTE]
> > `Enter_the_Supported_Account_Info_Here`

## <a name="more-information"></a>Más información

En esta sección se proporciona información general acerca del código necesario para el inicio de sesión de usuarios. Esto puede ser útil para comprender cómo funciona el código, los argumentos principales y también si desea agregar el inicio de sesión a una aplicación ASP.NET existente.

### <a name="how-the-sample-works"></a>Funcionamiento del ejemplo
![Muestra cómo funciona la aplicación de ejemplo generada por este inicio rápido.](media/quickstart-v2-aspnet-webapp/aspnetwebapp-intro.svg)

### <a name="owin-middleware-nuget-packages"></a>Paquetes NuGet del middleware OWIN

Puede configurar la canalización de autenticación con la autenticación basada en cookies mediante OpenID Connect en ASP.NET con paquetes del middleware OWIN. Puede instalar estos paquetes mediante la ejecución del siguiente comando en la **Consola del Administrador de paquetes** de Visual Studio:

```powershell
Install-Package Microsoft.Owin.Security.OpenIdConnect
Install-Package Microsoft.Owin.Security.Cookies
Install-Package Microsoft.Owin.Host.SystemWeb
```

### <a name="owin-startup-class"></a>Clase de inicio OWIN

El middleware OWIN usa una *clase startup* que se ejecuta cuando se inicializa el proceso de hospedaje. En este tutorial, el archivo *startup.cs* se encuentra en la carpeta raíz. En el código siguiente se muestra el parámetro utilizado por esta guía de inicio rápido:

```csharp
public void Configuration(IAppBuilder app)
{
    app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

    app.UseCookieAuthentication(new CookieAuthenticationOptions());
    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {
            // Sets the ClientId, authority, RedirectUri as obtained from web.config
            ClientId = clientId,
            Authority = authority,
            RedirectUri = redirectUri,
            // PostLogoutRedirectUri is the page that users will be redirected to after sign-out. In this case, it is using the home page
            PostLogoutRedirectUri = redirectUri,
            Scope = OpenIdConnectScope.OpenIdProfile,
            // ResponseType is set to request the id_token - which contains basic information about the signed-in user
            ResponseType = OpenIdConnectResponseType.IdToken,
            // ValidateIssuer set to false to allow personal and work accounts from any organization to sign in to your application
            // To only allow users from a single organizations, set ValidateIssuer to true and 'tenant' setting in web.config to the tenant name
            // To allow users from only a list of specific organizations, set ValidateIssuer to true and use ValidIssuers parameter
            TokenValidationParameters = new TokenValidationParameters()
            {
                ValidateIssuer = false // Simplification (see note below)
            },
            // OpenIdConnectAuthenticationNotifications configures OWIN to send notification of failed authentications to OnAuthenticationFailed method
            Notifications = new OpenIdConnectAuthenticationNotifications
            {
                AuthenticationFailed = OnAuthenticationFailed
            }
        }
    );
}
```

> |Where  | Descripción |
> |---------|---------|
> | `ClientId`     | El identificador de la aplicación registrada en Azure Portal |
> | `Authority`    | El punto de conexión STS para el usuario que se autenticará. Normalmente es `https://login.microsoftonline.com/{tenant}/v2.0` para la nube pública, donde {tenant} es el nombre del inquilino, el identificador del inquilino o *common* para hacer referencia al punto de conexión común (que se usa para las aplicaciones multiinquilino) |
> | `RedirectUri`  | Dirección URL a la que se envían a los usuarios después de la autenticación en la plataforma de identidad de Microsoft |
> | `PostLogoutRedirectUri`     | Dirección URL a donde se redirige a los usuarios después de cerrar sesión |
> | `Scope`     | La lista de ámbitos que se solicitan, separados por espacios |
> | `ResponseType`     | La solicitud para que la respuesta de la autenticación contenga un token de identificador |
> | `TokenValidationParameters`     | Una lista de parámetros para la validación del token. En este caso, `ValidateIssuer` está establecido en `false` para indicar que puede aceptar inicios de sesión desde cualquier tipo de cuenta: personal, profesional o educativa |
> | `Notifications`     | Una lista de delegados que se pueden ejecutar en diferentes mensajes de *OpenIdConnect* |


> [!NOTE]
> Establecer `ValidateIssuer = false` es una simplificación para este inicio rápido. En las aplicaciones reales, valide el emisor.
> Consulte los ejemplos para entender cómo hacerlo.

### <a name="initiate-an-authentication-challenge"></a>Inicio de un desafío de autenticación

Puede forzar a un usuario para que inicie sesión si solicita un desafío de autenticación en el controlador:

```csharp
public void SignIn()
{
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge(
            new AuthenticationProperties{ RedirectUri = "/" },
            OpenIdConnectAuthenticationDefaults.AuthenticationType);
    }
}
```

> [!TIP]
> Solicitar un desafío de autenticación mediante el método anterior es opcional y, normalmente, se utiliza cuando desea que exista una vista accesible tanto para los usuarios autenticados como para los que no lo están. También puede proteger los controladores mediante el método descrito en la sección siguiente.

### <a name="protect-a-controller-or-a-controllers-method"></a>Protección de un controlador o del método de un controlador

Puede proteger un controlador o las acciones de un controlador mediante el atributo `[Authorize]`. Este atributo restringe el acceso al controlador o a sus acciones al permitirle el acceso solo a los usuarios autenticados, por lo que el desafío de autenticación se realizará automáticamente cuando un usuario *sin autenticar* intente acceder a una de las acciones o controladores con el atributo `[Authorize]`.

[!INCLUDE [Help and support](../../../includes/active-directory-develop-help-support-include.md)]

## <a name="next-steps"></a>Pasos siguientes

Visite el tutorial de ASP.NET para acceder a una guía completa paso a paso sobre la creación de aplicaciones y nuevas características, que incluye una explicación completa de esta guía de inicio rápido.

> [!div class="nextstepaction"]
> [Incorporación del inicio de sesión a una aplicación web ASP.NET](tutorial-v2-asp-webapp.md)
