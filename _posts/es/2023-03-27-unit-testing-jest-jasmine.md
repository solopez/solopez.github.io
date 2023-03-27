---
date: 2023-03-27 8:00:00
layout: post
title: Unit testing Jest & Jasmine
description: Conceptos y ejemplos!
language: es
image: "../assets/img/jasmine_jest.jpg"
category: CODE
tags:
  - unit testing
  - jest
  - jasmine
  - humor
author: sol lopez
---

# Unit testing - Jasmine & Jest

Buenas! como andan? El post de hoy va dedicado a unit testing general teniendo en cuenta algunos conceptos y experiencias en ambos frameworks: Jasmine y Jest.

## mockReturnValue y mockReturnValueOnce

Supongamos un escenario donde queremos probar qué sucede cuando un método de algun servicio, retorna diferentes valores.
Un ejemplo clásico que podríamos usar sería el siguiente:

```typescript
jest.spyOn(userService, "get").mockReturnValue(0);
```

Ahora, si quisiéramos retornar otros valores para distintas llamadas al método, podemos hacer esto:

```typescript
jest
  .spyOn(userService, "get")
  .mockReturnValue(0) // default
  .mockReturnValueOnce(2) // first call
  .mockReturnValueOnce(4); // second call

it("should mock the return value of consecutive calls differently", () => {
  expect(userService.get()).toBe(2);
  expect(userService.get()).toBe(4);
  expect(userService.get()).toBe(0);
  expect(userService.get()).toBe(0);
});
```

Como se puede ver, con la función mockReturnValue retornaremos por "default" un valor, y si concatenamos con la función mockReturnValue**Once**, el once nos da la clave de que sólo retornará una única vez ese valor, y será según el orden que le demos.
Como vemos en el ejercicio, la primer llamada retornará 2, luego 4 y luego, todas las veces que lo sigamos llamando, siempre retornará 0 (default).

## **mockImplementation** y **mockImplementationOnce**

Del mismo modo que hicimos antes, podríamos concatenar distintos comportamientos por cada vez que se llame/invoque al método.
Es decir, podríamos hacer exactamente el mismo ejercicio anterior pero usando la función mockImplementation(), o también customizarlo un poco si así lo quisiéramos, por ejemplo:

```typescript
it("Should mock the return value of consecutive calls differently", () => {
  userService.get = jest
    .fn()

    .mockImplementation(() => 0) // default

    .mockImplementationOnce((num) => num + 10) // first call

    .mockImplementationOnce((num) => num + 20); // second call

  expect(userService.get(10)).toBe(20);

  expect(userService.get(10)).toBe(30);

  expect(userService.get()).toBe(0);

  expect(userService.get()).toBe(0);
});
```

Como vemos en este ejercicio, es posible realizar una suma diferente en cada llamada o invocación a nuestro método. Lo útil del mockImplementation es que al recibir una función como parámetro, debemos usarlo sabiamente, ya que con esta función es posible re-escribir cualquier lógica.

## Jasmine

Este mismo ejercicio de retornar distintos valores en llamadas consecutivas, en Jasmine también es posible, usando las funciones **returnValue** y **returnValues** .
En el caso de returnValue() devolveremos un sólo valor, mientras que en el caso de returnValues() podremos retornar distintos valores separados por coma y en ese orden.
Quedaría de la siguiente manera:

```typescript
spyOn(userService, "get").and.returnValues(2, 4, 0);
```

También, si quisiéramos obtener el equivalente de mockImplementation(), en Jasmine se podría hacer con la función callFake(), que también recibe como parámetro una función:

```typescript
spyOn(obj, "methodName").and.callFake(customImplementation);
```

## Limpieza de Spies

![Create comics meme "the shining memes, here's johnny, Jack Nicholson the  shining door" - Comics - Meme-arsenal.com](https://www.meme-arsenal.com/memes/06ec1715360623bb409a354cd5f36bd1.jpg)
En Jest, si quisiéramos limpiar los spies que vamos mockeando en cada escenario, podemos usar alguna de las 3 funciones que nos provee este framework: mockClear(), mockReset() y mockRestore().
Veamos como funcionan

```typescript
const spy = jest.spyOn(userService, "get");

spy.mockImplementation(() => "mocked implementation");

userService.get();

expect(spy).toHaveBeenCalledTimes(1); //mocked implementation

spy.mockClear();

userService.get();

expect(spy).toHaveBeenCalledTimes(1); //mocked implementation

spy.mockReset();

userService.get();

expect(spy).toHaveBeenCalledTimes(1); //undefined (reset destruye mockImplementation)

spy.mockRestore();
userService.get();
expect(spy).toHaveBeenCalledTimes(0); //Its me Mario!(implementación (stub) en provider)
```

El primer caso, **mockClear()** lo que hará será limpiar toda la información de tracking que nuestro spy almacena, pero mantendrá las mismas características de nuestro spy. En este caso, seguirá retornando lo que mockeamos mediante _mockImplementation()_.

El segundo caso, **mockReset()**, no sólo eliminará la información de tracking al igual que el clear, sino que también destruirá el mockeo que hayamos implementado, y lo reemplazará por undefined. Lo que significa que para poder continuar usando ese spy, deberemos volver a mockearlo según lo que necesitemos probar.

El tercer caso, **mockRestore()**, ya dejará de ser un spy, e invocará a nuestro método e implementación real. Es por eso que en este caso, el \*_toHaveBeenCalledTimes_(0)\* será 0, ya que el spy no se llama y directamente se ejecutaría la implementación real del método.

También es posible que usemos estas 3 funciones pero generales para todos los spies, en lugar de cada uno, para poder invocarlas por ejemplo, en los before/afterEach yo before/afterAll, de esta manera:

```typescript
jest.clearAllMocks();

jest.resetAllMocks();

jest.restoreAllMocks();
```

## Spies: Jasmine vs Jest

Un tema fundamental a tener en cuenta es que en Jasmine, y en la mayoría de los frameworks de testing, haciendo lo siguiente:

```typescript
    spyOn(obj, ‘methodName’); //!real function
```

Vemos que basta con sólo crear el spy de un método, para mockearlo, y que la implementación real no sea accesible por éste. De tal manera que cuando invoquemos nuestro método, éste no accederá a su implementación real, como si estuviera vacío.

Sin embargo, en Jest, es todo lo contrario:

```typescript
    jest.spyOn(obj, ‘methodName’); //real function
```

Cuando creamos el spy, no es suficiente y si invocamos al método, la implementación real es la que va a ir a buscar. Es por eso que en el caso de Jest, debemos aplicar algunas de las funciones de mockeo que nos provee el framekwork.

## Mockeando dependencias

![MOCKS: What are they? When should you use them?](https://media.licdn.com/dms/image/C4E12AQFFdpXrcMl4hg/article-cover_image-shrink_600_2000/0/1520175912857?e=2147483647&v=beta&t=M-q9AA8fseLznsSmQyfc8il3RgYH38ycq07V5J1vd5U)
Para mockear nuestras dependencias/servicios, basta con inyectarlo en nuestros tests de alguna de las siguientes maneras:

```typescript
    TestBed.configureTestingModule({
    providers: [

    { provide:  service, useClass:  serviceClassMock }

    { provide:  service, useValue: { serviceMock } }

    { provide:  service, useFactory: () => {
        if (IS_A) {
          return new A();
        } else {
          return new B();
        }
      }
```

En el primer caso _useClass_ , usaremos una instancia de una clase. En el segundo caso _useValue_, usaremos un objeto o valor estático. Y en el tercer caso _useFactory_ usaremos una función que pueda producir el valor a inyectar.

En el caso de una dependencia que no sea inyectada por constructor, sino directamente en un componente, de esta manera:

```typescript
    @Component({

    templateUrl:  './main.component.html',

    styleUrls: ['./main.component.scss'],

    providers: [service]

    })
```

Para poder mockear esa dependencia (scoped), vamos a necesitar aplicar la función overrideComponent(), de la siguiente manera:

```typescript
    TestBed.configureTestingModule({

    //imports, declarations, providers, schemas

    })

    .overrideComponent(MainComponent, { set: { providers:

    [{ provide:  service, useClass:  serviceClassMock }]

    }})

    .compileComponents()});
```

Implementando esa función, podremos inyectar nuestra dependencia con su respectivo mock.

## Conclusión

Viendo algunos conceptos y experiencias para continuar armando y mockeando nuestros tests, también es necesario tener en cuenta algunos puntos cuando escribimos tests:

- Tests simples, claros y descriptivos en los mensajes: la idea es que seamos tan claros que la próxima persona que lea nuestro test, pueda interpretar fácilmente qué se está probando y no tenga que ir a leer toda la suite de tests para poder hacerlo.
  ![Meme: "I think it is crystal clear" - All Templates - Meme-arsenal.com](https://www.meme-arsenal.com/memes/4b6a7e7edd3a8872aedda1060b276b87.jpg)

- Tests aislados, sin dependencias ni orden de ejecución: recordemos siempre mockear todas las dependencias y que nuestros tests deben arrojar siempre los mismos resultados, independientemente del orden en el que se ejecuten.
- Regla AAA: Arrange, Act, Assert: para una mejor legibilidad resulta útil poder desglosar y separar las 3 acciones en cada uno de nuestros tests.
- Exponer bugs: desde nuestros unit tests, es posible recrear los escenarios para poder reproducir los bugs que se hayan detectado, revelando los mismos, nos puede ser de mucha ayuda para detectar dónde se encuentra el problema y así poder fixear el código. También nos da mayor seguridad tener el unit test del escenario que estamos fixeando para garantizar que tal bug no regrese a la vida :)
  ![Don't be a mindless zombie this Halloween](https://www.evolutionrecruit.co.uk/wp-content/uploads/2018/10/zombie-hands-emerging-from-the-grave_4jxo6n6q__F0010.png)
  Happy coding!
