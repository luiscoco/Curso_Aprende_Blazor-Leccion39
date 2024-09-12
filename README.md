# CURSO: APRENDE BLAZOR

# LECCIÓN 39: Interoperatibilidad con JavaScript (librería SweetAlert2)

1. Abrir la aplicación con Visual Studio 2022 o VSCode

2. Creamos el archivo "example.js" donde definimos nuestra función de JavaScript a invocar desde C#. Localizamos el archivo dentro de una carpeta "js" localizada en "wwwroot"

```javascript
window.ShowSwal = function (type, message) {
    if (type == "success")
    {
        Swal.fire({
            title: "Good job!",
            text: "You clicked the button!",
            icon: "success"
        });
    }
    if (type == "error") {
        Swal.fire({
            icon: "error",
            title: "Oops...",
            text: "Something went wrong!",
            footer: '<a href="#">Why do I have this issue?</a>'
        });
    }
}
```

3. Creamos el nuevo componente para invocar desde C# la función toastrInterop() de JavaScript

```razor
@page "/sweetalert2"
@inject IJSRuntime JSRuntime

<h3>SweetAlert2 Notification Example</h3>

@* https://sweetalert2.github.io/ *@

<button @onclick="ShowSuccessNotification">Show Success</button>
<button @onclick="ShowErrorNotification">Show Error</button>

@code {
    private async Task ShowSuccessNotification()
    {
        // Call the JavaScript function to show a success message
        await JSRuntime.InvokeVoidAsync("ShowSwal", "success", "Success Notification");
    }

    private async Task ShowErrorNotification()
    {
        // Call the JavaScript function to show an error message
        await JSRuntime.InvokeVoidAsync("ShowSwal", "error", "Error Notification");
    }
}
```

4. Incluimos en el componente App.razor la localización de nuestro archivo example.js

```html
<script src="https://cdn.jsdelivr.net/npm/sweetalert2@11"></script>
```

5. Creamos un nuevo NavLink en el componente NavMenu.razor para navegar hacia nuestro nuevo componente

```razor
<div class="nav-item px-3">
     <NavLink class="nav-link" href="sweetalert2">
          <span class="bi bi-list-nested-nav-menu" aria-hidden="true"></span> SweetAlert2
     </NavLink>
</div>
```
6. Ejecutamos la aplicación
