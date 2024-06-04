
Los formularios son una característica muy común que se usan en cualquier aplicación.

En esta guía, vais a aprender sobre las dos técnicas utilizadas por Angular para crear formularios: formularios basados ​​en plantillas (Template Forms)y formularios reactivos (Reactive Forms).

Aparte de ello, también veremos cómo podemos agregar validaciones usando ambos enfoques.

Una vez terminado Gestión de datos , la aplicación tienda en línea tiene un catálogo de productos y un carrito de compras.

Esta sección te guía para agregar una funcionalidad de pago con un formulario para capturar los datos del usuario.

## Formularios en Angular

Los formularios en Angular están construidos sobre el formulario HTML estándar, para ayudarte a crear controladores personalizados y simplificar la experiencia de validación de campos. Un formulario reactivo en Angular se compone de dos partes: los objetos que viven en el componente para almacenar y gestionar el formulario, y la visualización que vive en la plantilla.
## Definir el modelo del formulario de pago


Primero, configura el modelo del formulario de pago. Se define en el componente clase, este modelo es la fuente de la verdad para el estado del formulario.

1. Abre `cart.component.ts`.
    
2. El servicio de Angular `[FormBuilder](https://docs.angular.lat/api/forms/FormBuilder)` proporciona los métodos para crear los controladores. Tal como otros servicios que hayas usado, necesitas importar e inyectar el servicio antes de usarlo:
    
    1. Importar `[FormBuilder](https://docs.angular.lat/api/forms/FormBuilder)` del módulo `@angular/forms`.
        
        src/app/cart/cart.component.ts
        
        content_copy`import { [Component](https://docs.angular.lat/api/core/Component), [OnInit](https://docs.angular.lat/api/core/OnInit) } from '@angular/core'; import { [FormBuilder](https://docs.angular.lat/api/forms/FormBuilder) } from '@angular/forms'; import { CartService } from '../cart.service';`
        
    
    El módulo `[ReactiveFormsModule](https://docs.angular.lat/api/forms/ReactiveFormsModule)` proporciona el servicio `[FormBuilder](https://docs.angular.lat/api/forms/FormBuilder)`, ya ha importado `AppModule` (en `app.module.ts`).
    
    2. Inyecta el servicio `[FormBuilder](https://docs.angular.lat/api/forms/FormBuilder)`.
        
        src/app/cart/cart.component.ts
        
        content_copy`export class CartComponent implements [OnInit](https://docs.angular.lat/api/core/OnInit) { items; constructor( private cartService: CartService, private formBuilder: [FormBuilder](https://docs.angular.lat/api/forms/FormBuilder), ) { } ngOnInit() { this.items = this.cartService.getItems(); } }`
        
3. En la clase `CartComponent`, define la propiedad `checkoutForm` para almacenar el modelo del formulario.
    

src/app/cart/cart.component.ts

content_copy`export class CartComponent implements [OnInit](https://docs.angular.lat/api/core/OnInit) { items; checkoutForm; }`

4. Para capturar el nombre y la dirección del usuario, configura la propiedad `checkoutForm` usando el método `group()` de `[FormBuilder](https://docs.angular.lat/api/forms/FormBuilder)` a un formulario que contenga los campos `name` y `addess`. Agrega esto entre las llaves, `{}`, del constructor.
    
    src/app/cart/cart.component.ts
    
    content_copy`export class CartComponent implements [OnInit](https://docs.angular.lat/api/core/OnInit) { items; checkoutForm; constructor( private cartService: CartService, private formBuilder: [FormBuilder](https://docs.angular.lat/api/forms/FormBuilder), ) { this.checkoutForm = this.formBuilder.group({ name: '', address: '' }); } ngOnInit() { this.items = this.cartService.getItems(); } }`
    
5. Para el proceso de pago, el usuario debe enviar el nombre y la dirección. Una vez enviada la orden se debe limpiar el formulario y el carrito.
    
    1. En `cart.component.ts`, define un método `onSubmit()` para procesar el formulario. Usa el método `clearCart()` de `CartService` para eliminar los elementos del carrito y restaurar el formulario después de enviarlo. En una aplicación de la vida real, este método también debe enviar los datos a un servidor externo. Por último el componente completo se vería así:
    
    src/app/cart/cart.component.ts
    
    content_copy`import { [Component](https://docs.angular.lat/api/core/Component), [OnInit](https://docs.angular.lat/api/core/OnInit) } from '@angular/core'; import { [FormBuilder](https://docs.angular.lat/api/forms/FormBuilder) } from '@angular/forms'; import { CartService } from '../cart.service'; @[Component](https://docs.angular.lat/api/core/Component)({ selector: 'app-cart', templateUrl: './cart.component.html', styleUrls: ['./cart.component.css'] }) export class CartComponent implements [OnInit](https://docs.angular.lat/api/core/OnInit) { items; checkoutForm; constructor( private cartService: CartService, private formBuilder: [FormBuilder](https://docs.angular.lat/api/forms/FormBuilder), ) { this.checkoutForm = this.formBuilder.group({ name: '', address: '' }); } ngOnInit() { this.items = this.cartService.getItems(); } onSubmit(customerData) { // Process checkout data here this.items = this.cartService.clearCart(); this.checkoutForm.reset(); console.warn('Your order has been submitted', customerData); } }`
    

Habiendo definido el modelo del formulario en el componente, necesitas un formulario de pago que refleje el modelo en la vista.

## Crear el formulario de pago

Sigue estos pasos para agregar un formulario de pago en la sección inferior de la vista del componente "Cart".

1. Abre `cart.component.html`.
    
2. Al final de la plantilla agrega un formulario HTML para capturar los datos del usuario.
    
3. Usa el enlace de propiedades de `formGroup` para enlazar el `checkoutForm` a la etiqueta `form` en la plantilla. También agrega un botón 'Comprar' para enviar el formulario.
    
    src/app/cart/cart.component.html
    
    content_copy`<form [formGroup]="checkoutForm"> <button class="button" type="submit">Purchase</button> </form>`
    
4. En la etiqueta form, usa el evento `ngSubmit` para escuchar el envío del formulario e invocar el método `onSubmit()` con el valor `checkoutForm`.
    
    src/app/cart/cart.component.html (cart component template detail)
    
    content_copy`<form [formGroup]="checkoutForm" (ngSubmit)="onSubmit(checkoutForm.value)"> </form>`
    

REFERENCIAS:

- [https://mugan86.medium.com/formularios-en-angular-diferencias-template-y-reactive-forms-e37af5e30b81](https://mugan86.medium.com/formularios-en-angular-diferencias-template-y-reactive-forms-e37af5e30b81)
- [https://docs.angular.lat/start/start-forms#formularios-en-angular](https://docs.angular.lat/start/start-forms#formularios-en-angular)

Link del VIDEO: [https://youtu.be/wd_97XEtqRo](https://youtu.be/wd_97XEtqRo)