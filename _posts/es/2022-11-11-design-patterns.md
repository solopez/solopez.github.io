---
date: 2022-11-11 9:00:40
layout: post
title: Patrones de diseño!
description: En el post de hoy explicación y ejemplos de patrones de diseño.
language: es
image: '../assets/img/design_patterns.png'
category: CODE
tags:
  - coding
  - design patterns
  - humor
author: sol lopez
---


# Patrones de diseño

Para desarrollar aplicaciones de calidad vamos a necesitar tener un buen conocimiento de los patrones de diseño existentes, de esta manera, podremos reconocer cuándo es posible utilizarlos en nuestros proyectos. 
Los patrones de diseño surgen para ayudarnos a resolver tareas comunes de desarrollo de una manera específica, para que no reinventemos la rueda, aprendamos y fomentemos las buenas prácticas, estandaricemos la resolución de determinados problemas, etc. También están clasificados en 3 categorías: creacionales, estructurales y de comportamiento.
Además, en el post de hoy voy a relacionar algunos patrones con proyectos en Angular.

![enter image description here](https://www.happierhuman.com/wp-content/uploads/2022/04/happy-memes-winkgo-oh-my-god.jpg)

## Patrón MVC-MVVM

El patrón de diseño MVC refiere a la arquitectura de nuestra app, donde existen tres partes diferenciadas. 
Los modelos se utilizan para representar los datos (por ej. interfaz o clase sin lógica). 
Las vistas corresponden a la interfaz de usuario (el modelo HTML). 
Finalmente los controladores/componentes permiten enlazar las dos capas anteriores. 
Sin embargo, como sabemos, Angular soporta two-way data binding, por lo que podríamos decir que en realidad estamos usando MVVM (Model-View-ViewModel). 
[Acá](https://medium.com/@maaouikimo/why-angular-is-your-best-choice-for-you-next-projects-9d754fb18f91) te dejo más info complementaria de esto.
![enter image description here](https://miro.medium.com/max/619/1*LRTtsieSkeFseiWD4f9DDA.png)

## Patrón de inyección de dependencias

La inyección de dependencias (DI) es un patrón de diseño importante para el desarrollo de aplicaciones a gran escala. Angular tiene su propio sistema DI, lo que aumenta la eficiencia y la escalabilidad. Si recuerdan, en los constructores de nuestras clases (componentes, directivas, servicios) se inyectan las dependencias (servicios u objetos), así como también éstas se pueden proveer. Algunos ejemplos de la guía oficial [acá](https://angular.io/guide/dependency-injection). 


## Principios SOLID

Los principios SOLID es un conjunto de **cinco principios** adecuados para la programación orientada a objetos. Su objetivo es hacer que el diseño del software sea más comprensible, flexible y mantenible. Estos principios permiten destacar las buenas prácticas a seguir, pero son abstractos, por lo que existen varios patrones concretos para desarrollar respetando estos principios.

![enter image description here](https://miro.medium.com/max/1191/1*OzwARbvHUg1RlZ7LYyLCrg.png)

 1. Responsabilidad única: Cada archivo (clase / función / módulo / sección) debe tener una sola responsabilidad, es decir, debe permitir hacer una sola cosa. Por lo tanto, debemos dividir la lógica en tantas clases y archivos como sea necesario. Además debe haber un lugar para todos los tipos de archivos y cada archivo debe estar en el lugar correcto.
 
 2. Abierto-cerrado: Cada clase debe estar abierta para su ampliación, pero cerrada para su modificación. Debe ser posible ampliar la funcionalidad sólo añadiendo código pero sin cambiar el código existente. Esto es para minimizar el riesgo de romper la lógica.

 3. Sustitución de Liskov: Si B y C son implementaciones de A, entonces B y C deben poder intercambiarse sin afectar a la ejecución del programa. Las implementaciones de B y C deben tener las mismas funciones, firmas y tipos para poder intercambiarlas. (Ejemplo: patrón de estrategia que podemos profundizar en otro post)
  ![enter image description here](https://blog.codavel.com/hubfs/Imported_Blog_Media/LiskovSubtitutionPrinciple_Simon.jpg)

 4. Principio de segregación de interfaces: Si B y C son implementaciones de A, entonces B y C deben ser realmente capaces de implementar las funciones descritas en la interfaz A. Al ejecutar nuestro programa no debemos comprobar si la implementación puede activar este método. Si este es el caso, la solución es dividir en varias interfaces.

 5. Principio de inversión de la dependencia: Los módulos de alto nivel no deberían depender de los de bajo nivel, sino que ambos deberían depender de las abstracciones. (Ej: patrón de inyección de dependencia)

Nota: armaré otros posts para profundizar cada uno de ellos.


## Patrón Strategy
Clasificación: Comportamiento
El patrón de diseño de estrategia implica separar la ejecución de una lógica de negocio de la entidad que la utiliza y dar a esa entidad una forma de cambiar entre diferentes formas de lógica. Por ejemplo, para poder realizar diferentes tipos de ordenación en una entidad, debes crear una clase o función abstracta SortingStrategy y luego crear diferentes implementaciones de ordenación. Ahora puedes seleccionar la estrategia cambiando entre las diferentes implementaciones en función de tus necesidades.
Nota: este amerita un post exclusivo, coming soon...
![enter image description here](https://s3.memeshappen.com/memes/Coming-soon--meme-45738.jpg)

## Patrón de composición
Clasificación: Estructural
La herencia ofrecida por la programación orientada a objetos puede crear objetos jerárquicos muy acoplados que son difíciles de refactorizar, debido a las dependencias de los objetos. Es por eso que podemos usar este patrón de composición para poder permitir la flexibilidad en lo que el objeto contenedor puede hacer. Básicamente estamos hablando de poder **agrupar** nuestros componentes, y sub-agrupar también, generando una specie de árbol en lo que respecta a estructura de datos.
Para decirlo en criollo, podemos tener productos, que pueden ser guardados en cajas. Y a su vez, tener cajas dentro de otras cajas. Si tenés un caso con múltiples objetos usando la misma interfaz, puede que este sea el patrón que te ayude a simplificar esa interacción entre ellos.

Vamos al código (referencias [acá](https://blog.bitsrc.io/design-patterns-in-typescript-e9f84de40449))

    interface IProduct {
	    getName(): string
        getPrice(): number
    }
    
    //The "Component" entity
    
    class Product implements IProduct {
    
    private price:number
    
    private name:string
    
    constructor(name:string, price:number) {
    
    this.name = name
    
    this.price = price
    
    }
    
    public getPrice(): number {
    
    return this.price
    
    }
    
    public getName(): string {
    
    return this.name
    
    }
    
    }
    
    //The "Composite" entity which will group all other composites and components (hence the "IProduct" interface)
    
    class Box implements IProduct {
    
    private products: IProduct[] = []
    
    contructor() {
    
    this.products = []
    
    }
    
    public getName(): string {
    
    return "A box with " + this.products.length + " products"
    
    }
    
    add(p: IProduct):void {
    
    console.log("Adding a ", p.getName(), "to the box")
    
    this.products.push(p)
    
    }
    
    getPrice(): number {
    	    return this.products.reduce( (curr: number, b: IProduct) => (curr + b.getPrice()), 0)
        }
    }
    
    //Using the code...
    
    const box1 = new Box()
    
    box1.add(new Product("Bubble gum", 0.5))
    
    box1.add(new Product("Samsung Note 20", 1005))
    
    const box2 = new Box()
    
    box2.add( new Product("Samsung TV 20in", 300))
    
    box2.add( new Product("Samsung TV 50in", 800))
    
    box1.add(box2)
    
    console.log("Total price: ", box1.getPrice())


## Patrón Lazy

El patrón de diseño lazy permite desarrollar aplicaciones escalables y de alto rendimiento porque el principio de este patrón es proporcionar una aplicación dividida en partes independientes. Esto permite reducir el tamaño de la aplicación principal y disponer de diferentes módulos que serán únicamente descargados por el usuario sólo accede a esa parte específica de la app.

## Patrón Singleton
Clasificación: Creacional
Este patrón garantiza que sólo haya una instancia de tu clase. Gracias a este singleton, se puede controlar el alcance de las variables en su interior. El singleton se maneja mediante un método público getInstance que garantiza la única forma de acceder a la clase. 
En Angular, el mecanismo de inyección de dependencia gestiona el patrón por nosotros. Por ejemplo, los servicios proporcionados en la raíz (root) de la aplicación son instancias singleton, por el contrario, los servicios proporcionados en los componentes **no** son singleton, y por lo tanto, serán instanciados por los componentes que lo inyecten.

## Patrón Factory

Clasificación: Creacional
Este patrón es muy simple pero muy útil cuando se necesita instanciar diferentes objetos hijos de la misma clase padre de acuerdo a ciertas condiciones. La fábrica define una interfaz de creación de objetos con las condiciones de creación como entrada y la instancia del objeto como salida. Esta interfaz suele contener un único método público. Entonces, es posible tener diferentes implementaciones de esta interfaz de fábrica, cada una con su propia lógica para instanciar los objetos. 
Nota: este patrón se aplica cuando hay lógica especial para instanciar los objetos hijos, sino no.

Por ejemplo, si alguna vez usaste o te suena de haber visto algo como:

    const componentRef = viewContainerRef.createComponent<AdComponent>(adItem.component);
    
   Eso es exactamente un factory desarrollado por Angular, y que nos lo brinda para poder implementar la carga de componentes dinámicamente. 
   Supongamos que queremos armar un componente de tipo Ad (publicidad) para mostrar banners, en lugar de generar templates estáticos con estos banners, podemos hacer uso de este factory para generar componentes que rendericen distintos contenidos para mostrar dinámicamente. 
   Te dejo la guía oficial con el código [acá](https://angular.io/guide/dynamic-component-loader).

## Patrón Decorator
Clasificación: Estructural
El patrón de diseño decorador es una alternativa a las subclases para extender un objeto utilizando la composición en lugar de la herencia. Entonces, la idea del decorador es poder agregar responsabilidades adicionales a un objeto. El concepto principal es tener un objeto que envuelva a otro objeto. El que envuelve al objeto es el decorador y es del **mismo tipo** que el objeto original pero también tiene un **objeto del mismo tipo** del objeto.

Por un lado tenemos el Typescript decorator (docu oficial [acá](https://www.typescriptlang.org/docs/handbook/decorators.html)):

Es un cambio único pero permanente, ya que la clase que se decora es diferente de la clase original. Y es simple, básicamente una **función**. Se da en tiempo de **compilación**. 

El escenario común es que un decorador se aplique a diferentes clases. Por ejemplo: en Angular, el decorador @injector se aplica a varias clases y las hace inyectables. También podemos hacer nuestros custom decorators, que quisiera profundizar con detalle en otro post.

Para el patrón general de decoradores:

El escenario común es diferentes decoradores en una sola clase. Necesitamos crear una clase decoradora, una clase padre común para la clase decoradora y la clase original, y diferentes clases decoradoras hijas. La clase original permanece sin cambios y se puede aplicar el decorador como se considere oportuno durante el tiempo de **ejecución**.

Ejemplo: tenemos una clase café. Podemos crear diferentes clases decoradoras: Espresso , Cappuccino, pero también podemos mezclar y combinarlas: café expreso + Cappuccino.

Veamos un ejemplo de código (dejo referencia y más info [acá](https://blog.bitsrc.io/design-patterns-in-typescript-e9f84de40449)):

    abstract class Animal {
    
    abstract move(): void
    
    }
    
    abstract class SuperDecorator extends Animal {
    
    protected comp: Animal
    
    constructor(decoratedAnimal: Animal) {
    
    super()
    
    this.comp = decoratedAnimal
    
    }
    
    abstract move(): void
    
    }
    
    class Dog extends Animal {
    
    public move():void {
    
    console.log("Moving the dog...")
    
    }
    
    }
    
    class SuperAnimal extends SuperDecorator {
    
    public move():void {
    
    console.log("Starts flying...")
    
    this.comp.move()
    
    console.log("Landing...")
    
    }
    
    }
    
    class SwimmingAnimal extends SuperDecorator {
    
    public move():void {
    
    console.log("Jumps into the water...")
    
    this.comp.move()
    
    }
    
    }
    
    const dog = new Dog()
    
    console.log("--- Non-decorated attempt: ")
    
    dog.move()
    
    console.log("--- Flying decorator --- ")
    
    const superDog = new SuperAnimal(dog)
    
    superDog.move()
    
    console.log("--- Now let's go swimming --- ")
    
    const swimmingDog = new SwimmingAnimal(dog)
    
    swimmingDog.move()


# Conclusión
Poder conocer algunos de los patrones de diseño que existen, nos brinda muchas oportunidades no sólo para mejorar en lo que hacemos, sino para poder simplificar y resolver problemas que podemos encontrar a diario. 

Referencias de este post y para complementar por [acá!](https://angular-enterprise.com/en/ngpost/courses/design-patterns/)

Happy coding!
![enter image description here](https://bemorepanda.com/files/2020-12-19/images/297058.jpeg)

