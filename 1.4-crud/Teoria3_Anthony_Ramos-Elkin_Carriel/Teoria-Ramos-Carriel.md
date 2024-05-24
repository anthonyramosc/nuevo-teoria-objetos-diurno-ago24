youtube_url: https://youtu.be/CKVU4vaUH6c 


# Servicios de Nest.js

 Los servicios son una pieza esencial de las aplicaciones realizadas con el framework
 NestJS. Están pensados para proporcionar una capa de acceso a los datos que
 necesitan las aplicaciones para funcionar. Mediante los servicios podemos liberar de código
 a los controladores y conseguir desacoplar éstos de las tecnologías de almacenamiento de
 datos que estemos utilizando.

 # Qué son providers

 Los providers están preparados para ser inyectados en los controladores de la
 aplicación, y otras clases si fuera necesario, a través del sistema de inyección de
 dependencias que proporciona Nest. Gracias a la inyección de dependencias es muy
 sencillo crear y proporcionar instancias de las clases a los controladores, delegando al
 propio Nest ese trabajo de instanciar las clases.
 Todos los providers que pensamos usar dentro de los módulos se tienen que
 declarar mediante el decorador @Module(). Esto no es un problema porque
 generalmente esta tarea se realizará automáticamente por el CLI al generar
 las clases inyectables