---
date: 2020-06-18 12:26:40
layout: post
title: Unit testing with Jasmine!
description: Reactive forms
image: '../assets/img/tests2.png'
category: test
language: en
tags:
  - jasmine
  - reactiveforms
  - humor
author: sol lopez

---
# Unit testing with Jasmine!
## Let's make some tests!

Hello! Continuing with unit testing... has it ever happened to you that the tests that contain a reactive form do not correctly instantiate the controls? Well, it will happen to them :O

Sometimes we are going to find this wonder:

     formGroup expects a FormGroup instance, please pass one in blah blah blah

Well, a lot of times you won't see this error if you mocked the whole gem at once, but if not... hello

What does this error mean?

If we run into this error, it simply means that the test fails to recognize any form instance of our component, that is, it fails to see that there is a form in our template and its association in TS.
![enter image description here](https://www.generadormemes.com/download/82iu845i7eevh1my3la94t5thtcbgwhkrp9fazs6m8pfdrq6ck21t0hjshlz0b9)

To start, let's review the basics that we must contemplate when building the base of our .spec of a form component:

In the imports, make sure that we have the following:

    imports: [ 
	    ReactiveFormsModule,
	    FormsModule


And if we have custom controls, add those modules too, for example
    imports: [
	    SelectModule
	    InputModule

Second, let's mock the values of the variables/arrays or wherever those controls consume in order to initialize. If we don't need to initialize, we can leave them empty or null, but always mock null from our .spec.

For example, in the case of a select, it will take the items from an array, we can mock the array or pass [] to it so that the control can be correctly instantiated.

Finally, we need to call our dear

     fixture.detectChanges();

This is necessary for our tests to run the angular init cycle and the template init, where we have our form.

![enter image description here](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSBjIp1tH1msYRzKrod0BjyHJbnwNhmMBO0WzHhXcZd3cAEZt3H&usqp=CAU)

Yes we have a BONUS!

If we want not only to mock the values to instantiate our form, but also to build our form builder as we please in the .spec, it is possible:

    let fixture: ComponentFixture<ChildComponent>;
     
    const formBuilder: FormBuilder = new FormBuilder();

and then:

    providers: [{ provide: FormBuilder, useValue: formBuilder }]

beforeEach:

    component.form = formBuilder.group({
	    firstName: null,
	    lastName: null
	});
    
    fixture.detectChanges();

![enter image description here](https://i.pinimg.com/originals/39/46/07/394607fdeea1f286afe8a4a0a28ec9fe.png)

By Sol López, frontend, rosarina, drummer, rock & metal.