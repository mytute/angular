
# Angular Tutorial

[Data Binding](#data-binding)    
[Property Binding](#property-binding)    
[Native Event Binding](#native-event-binding)    
[Two Way Data Binding](#two-way-data-binding)    
[Custom Property Binding](#custom-property-binding)    
[Custom Event Binding](#custom-event-binding)    
[Routing](#Routing)    
[Adding Links](#adding-links)    
[Route Params](#route-params)    
[Routing](#Routing)    
[Directive Introduction](#directive-introduction)    
[ngFor](#ngfor)
[ng-template](#ngTemplate)
[get data from api](#get-data-from-api)
[angular deploy with node js](#angular-deploy-with-node-js)
[uninstall angular-cli](#uninstall-angular-cli)



installation
to work with angular should install node js to your os.    

to check node version    
$ node -v

to install angular cli globally    
$ npm install -g @angular/cli

to check angular version    
$ ng --version

to change angular version
```shell
ng --version
npm uninstall -g @angular/cli
npm cache clean --force

npm install -g @angular/cli@7.2.12
ng --version
```


to start new project
$ ng new <my-app-name>
   step run 1: type yes for add angular routes
   step run 2: select 'SCSS' for stylesheet format

to open location in VSCODE in terminal
$ code .

to start already created project
first you need go to location that have index file
$ ng serve -o
  '-o' option for open starting project on browser

to create new component
$ ng generate component <component-name>


to create new service
$ ng generate service <service-name>





# Data Binding

### data transfer from file.ts to file.html in same component


>file.ts

```javascript
import { Component, OnInit } from '@angular/core';


@Component({
  selector: 'app-home',
  templateUrl: './home.component.html',
  styleUrls: ['./home.component.css']
})
export class HomeComponent implements OnInit {
  homeTitle = "this data from homeComponent class";

  constructor() { }

  ngOnInit(): void {
  }

}
```

>file.html  

```html
<p>{{homeTitle}}</p>
```

# Property Binding

### data transfer from file.ts to file.html in same component

This thing can do with previous method too.    
```html
<input value="{{myString}}" />
```
But as a improvment here we are use '[property_name ]' to get this property name's value from file.ts.    
```html
<input [property_name ]="value_variable_located_in_ts_file" />
```

### Binding to HTML properties
  * Native HTML properties: [value]="express"   
      ```html
         <input value="type some thing" />
      ```
  * Custom-made properties: [myProp]="express"   
      ```html
         <input count="true" />
      ```
  * Built in angular directives: [ngClass]="express"   
      ```html
         <input count="true" />  ????
      ```

### Binding to HTML properties  


>file.ts

```javascript
import { Component, OnInit } from '@angular/core';


@Component({
  selector: 'app-home',
  templateUrl: './home.component.html',
  styleUrls: ['./home.component.css']
})
export class HomeComponent implements OnInit {
  myString = "Enter value here";

  constructor() { }

  ngOnInit(): void {
  }

}
```

>file.html  

```html
<input [value]=myString/>
```

# Two Way Data Binding

### Here dynamically changing value from shared variable(ninja) that located in file.ts .(Binding in same component)

>file.ts

```javascript
import { Component, OnInit } from '@angular/core';


@Component({
  selector: 'app-home',
  templateUrl: './home.component.html',
  styleUrls: ['./home.component.css']
})
export class HomeComponent implements OnInit {

  public ninja = {
      name:"Yoshi",
      belt:"Black"
  };

  constructor() { }

  ngOnInit(): void {
  }

}
```

>file.html  

```html
<input [(ngModel)]="ninja.name" />
<p>{{ninja.name}}</p>
```
*  *space required ( "ninja.name" /> )*

* In html file when value change of input field then dynamically it change value of p tags.    
* "ngModel" is unique name binder for make communicate between file.ts and file.html .



# Native Event Binding

### Here we send click event from file.html to file.ts in same component. (Binding in same component)

>file.ts

```javascript
import { Component, OnInit } from '@angular/core';


@Component({
  selector: 'app-home',
  templateUrl: './home.component.html',
  styleUrls: ['./home.component.css']
})
export class HomeComponent implements OnInit {

  alertMe(val){
    alert(val);
  };

  constructor() { }

  ngOnInit(): void {
  }

}
```

>file.html  

```html
<button (click)="alertMe('i am good person')" > Click Me</button>
```


# Custom Property Binding

### Here we transfer data between two components.

we are using data sender component's html file as media of transferring between two components.     
data sending parent to child.     

>app.ts

```javascript
import { Component } from '@angular/core';
import { NgModule } from '@angular/core';

//import { ROUTER_DIRECTIVES } from "@/angular/router";

@Component({
  selector: 'app-root', /* selector of index.html*/
  templateUrl: './app.component.html', /**/
  /*template : '<h1>{{title}}</h1>',*/
  styleUrls: ['./app.component.css'],
  //directives : [ ROUTER_DIRECTIVES ]
})
export class AppComponent {

  public school ={
    name:"Asoka Collage",
    adress:"Colombo 10"
  };

}

```

>root.html  

```html
<app-home [prop]="school"  >Loading..</app-home>
```


>file.ts

```javascript
import { Component, OnInit , Input} from '@angular/core';

@Component({
  selector: 'app-home',
  templateUrl: './home.component.html',
  styleUrls: ['./home.component.css']
})
export class HomeComponent implements OnInit {

  @Input() prop;

  constructor() { }

  ngOnInit(): void {
  }

}
```

>file.html  

```html
<p>{{prop.name}}</p>
<p>{{prop.adress}}</p>
```
Finally we can represent data values from app.component.ts on home.component.html


# Custom Event Binding

### Here we make custom event among components.    
event sending child to parent.

In here we make app.html `(onYell)` event listen from home.ts using  
`@Output onYell = new EventEmitter()``

To control custom event `(onYell)` from different component we make native `(click)` event on home.html page and when if fire then it's inside function `fireYellEvent` we can `onYell.emit(e)` the custom function on app.html .

>app.ts (custom event's fire function )

```javascript
import { Component } from '@angular/core';
import { NgModule } from '@angular/core';

@Component({
  selector: 'app-root', /* selector of index.html*/
  templateUrl: './app.component.html', /**/
  /*template : '<h1>{{title}}</h1>',*/
  styleUrls: ['./app.component.css'],
  //directives : [ ROUTER_DIRECTIVES ]
})
export class AppComponent {
  //
  yell(e){
     alert("I am yelling...");
  }
}

```

>root.html  (custom event )

```html
 <app-home (onYell)="yell($event)" >Loading..</app-home>
```


>file.ts (make listem the custom event and make it's emit with click event)

```javascript
import { Component, OnInit , Input, Output , EventEmitter} from '@angular/core';

@Component({
  selector: 'app-home',
  templateUrl: './home.component.html',
  styleUrls: ['./home.component.css']
})
export class HomeComponent implements OnInit {

  /* make listener for custom event
     @Output() mean...
  */
  @Output() onYell = new EventEmitter();

  fireYellEvent(e){
    this.onYell.emit();
  }

  constructor() { }

  ngOnInit(): void {
  }

}

```

>file.html  (make native click event )

```html
<button (click)="fireYellEvent($event)" > Hit Me</button>
```

[Routing](#Routing)
# Routing

*  Here we declare routes in the `app-routing.module.ts` file.
*   The path: "" parameter relates to the url where the user will land when entered in the browser’s address bar.

* In first good to make new component

 ```bash
  $ ng generate component [name_of_component]
 ```
* When you are generate new component it will automatically will update with "declarations" and it's imports on `app.module.ts` file.

>app-routing.module.ts

```javascript
import { NgModule } from '@angular/core'; //#
import { Routes, RouterModule } from '@angular/router'; //#

// import your route files
import { HomeComponent } from "./home/home.component";
import { DirectoryComponent } from "./directory/directory.component";

// make your router path
const routes: Routes = [
  {
    path:'directory',
    component :DirectoryComponent,
  },
  {
    path:'', /* home  */
    component :HomeComponent,
  }
];


@NgModule({
  imports: [RouterModule.forRoot(routes)], //#
  exports: [RouterModule] //#
})
export class AppRoutingModule { } //#
```

following code show how to link our created routes on root.html file.

>root.html  (app.component.html)

```html
<!--   <app-home [prop]="school" (onYell)="yell($event)" >Loading..</app-home>  -->
<router-outlet> </router-outlet>
```



  URL pattern /heroes/:limit. Example: /heroes/20
      You can get raw value by using route.snapshot.paramMap.get.
      Subscribe from route.paramMap to get params

  URL pattern /heroes. Example: /heroes?limit=20
      You can get raw value by using route.snapshot.queryParamMap


# Adding Links

Following tutorial we are linking previous created routes on html page with two methods .
1. with normal  href html linking ( with reload hole page )
2. with special angular variables( non reload hole page )

```html
<header>
  <h1>{{title}}</h1>
  <nav>
    <ul>
      <!-- first method -->
      <li> <a href="/" >Home</a> </li>
      <li> <a href="/directory" >directory</a> </li>
      <li> <a href="/tables" >tables</a> </li>
    </ul>
    <ul>
      <!-- second method -->
      <li> <a [routerLink] ="['']" >Home</a> </li>
      <li> <a [routerLink] ="['directory']" >directory</a> </li>
      <li> <a [routerLink] ="['tables']" >tables</a> </li>
    </ul>
  </nav>
</header>

<section id="main">
   <!--   <app-home [prop]="school" (onYell)="yell($event)" >Loading..</app-home>  -->
   <router-outlet> </router-outlet>
</section>
```

# Route Params

* we are going to grap link parameter on 'tables' path.  
* first we need  add variable on 'tables' path in where we created routes(angular 9 > app-routing.module.ts ).

```javascript
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';

import { HomeComponent } from "./home/home.component";
import { DirectoryComponent } from "./directory/directory.component";
import { TableComponent } from "./table/table.component";

const routes: Routes = [
  {
    path:'directory',
    component :DirectoryComponent,
  },
  {
    path:'tables',
    component :TableComponent,
  },
  {
    path:'tables/:name', /*add> :name*/
    component :TableComponent,
  },
  {
    path:'', /* home  */
    component :HomeComponent,
  }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }

```


* secondly we need grep link variable from url

```javascript
import { Component, OnInit } from '@angular/core';
import { ActivatedRoute } from '@angular/router'  /*add> line */

@Component({
  selector: 'app-table',
  templateUrl: './table.component.html',
  styleUrls: ['./table.component.css']
})
export class TableComponent implements OnInit {
  ninja: string ;
  constructor( private route:ActivatedRoute ) {
    this.ninja = route.snapshot.params['name'];
    //console.log("param value :" ,this.ninja);
  }

  ngOnInit(): void {
  }

}

```

* lastly as working demonstration we can implement link variable value on "table.component.html"   

```html
    <p>table works!</p>
    <p>{{ninja}}</p>
```

# Directive Introduction

* Directives are instructions which tell Angular to do something.     
eg:
```html
    <router-outlet> </router-outlet>   
    [routerLink]=""
```    

There are two types of Directive
Attribute:
* Interacts with the element it's on to change it's properties.(eg:ngClass>change element class)
Structural:
* Change the structure of the HTML code.(eg:ngIf)

## Attribute Directive   

following example we use "ngClass" html element class selector on "file.component.html" page.

> file.component.html        

```html
<!-- ngClass class expection property here {}-->
<p [ngClass]="{'blue':false,'red':true,'underline':true}">directory works!</p>


<style>
  .blue{color:blue;}
  .red{color:red;}
  .underline{text-decoration: underline;}
</style>
```
even we can use this selector as property binder on "file.component.ts" file.advantage is we can dynamically change ngClass object on file.component.ts file.   

> file.component.html     

```html

<p [ngClass]="classes">directory works!</p>

<style>
  .blue{color:blue;}
  .red{color:red;}
  .underline{text-decoration: underline;}
</style>
```

> file.component.ts

```javascript
import { Component, OnInit } from '@angular/core';


@Component({
  selector: 'app-directory',
  templateUrl: './directory.component.html',
  styleUrls: ['./directory.component.css']
})
export class DirectoryComponent implements OnInit {
  classes = {'blue':true,'red':false,'underline':true };
  constructor( ) {

  }

  ngOnInit(): void {
  }

}
```

## Structural Directive  

```html

<p *ngIf="true">Only show if test it true </p>

```
this example also bind with variable from file.component.ts file for dynamically changes .

# ngFor


> home.ts      

```javascript

fruits: Array<string> = ['Apple', 'Orange', 'Banana'];

```

> home.html      

```javascript
<p *ngFor="let fruit of fruits; count as i;index as p" >
    {{fruit}} {{i}} <span></span>
</p>
```
you can use "span" tag inside p tags.
you can access ngFor variables using {{your_variable_inside_ngFor_condition}}   

# ngContent  

passing another template to child inside child template tag.    

>parent.tempate.html file

```html
<app-testcompo>
    <p #showme >samadhi laksahan piyasiri</p>
</app-testcompo>
```

>child.template.html file   

```html
<p >testcompo works!</p>
<ng-content></ng-content>
```

when we want access parent element within child element.
so we can use "@ContentChild" inside child compoent.ts file.
>child.component.ts file      

```typescript
import { AfterContentInit, Component, ContentChild, ElementRef, OnInit } from '@angular/core';

@Component({
  selector: 'app-testcompo',
  templateUrl: './testcompo.component.html',
  styleUrls: ['./testcompo.component.scss']
})
export class TestcompoComponent implements OnInit,AfterContentInit {

  constructor() { }

  @ContentChild('showme') public compo:ElementRef;

  ngOnInit(): void {
  }

  ngAfterContentInit():void{
    console.log('after content init in child :', this.compo);
  }

}
```

# ngTemplate

These template elements only work in the presence of structural directives.

different way to access ng-template.

1. by using structural directive.     
depend on ,mark>*ngIf</mark> directive it will show the ng-template.    

```html
<div *ngIf="false;else showTemplateOne;" >
    <p>no template </p>
</div>

<div *ngIf="true; then showTemplateTwo ;else showTemplateOne;" >
    <p>no template </p>
</div>

<ng-template #showTemplateOne >
    <p>show template one</p>
</ng-template>

<ng-template #showTemplateTwo >
    <p>show template two</p>
</ng-template>
```
2. passing data to ng template.    
you can pass n number of variables to ng-template.   
you can use <mark>div</mark> instead of <mark>ng-container</mark>.  

```html
<ng-container *ngTemplateOutlet="showTemplateOne; context:{ varOne : 'show template one', varTwo:'var two value'}">
    samadhi laksahan
</ng-container>

<ng-template #showTemplateOne let-varone="varOne" let-vartwo="varTwo">
    <p>{{varone}}</p>
    <p>{{vartwo}}</p>
</ng-template>
```
3. send data from component.ts file to ng-template.   
we need to add id for both tags for access from component.ts file.    

```html
<ng-container #placeholder> </ng-container>

<ng-template #showTemplate let-varone="varOne" let-vartwo="varTwo" >
     <p>{{ varone }}</p>
     <P>{{ vartwo }}</P>
</ng-template>
```

compoents.ts file  (static:true)

```typescript
import { Component, OnInit, TemplateRef, ViewChild, ViewContainerRef } from '@angular/core';

@Component({
  selector: 'app-main',
  templateUrl: './main.component.html',
  styleUrls: ['./main.component.scss']
})
export class MainComponent implements OnInit {

  constructor() { }

  @ViewChild('placeholder', {read : ViewContainerRef, static:true}) public container:ViewContainerRef;
  @ViewChild('showTemplate', {static:true}) public template:TemplateRef<any>;


  ngOnInit(): void {
    // because of we are using "static:true" we can use viewchild inside ngOnInit
    // otherwise we have to use "ngAfterViewInit"
    this.container.createEmbeddedView(this.template, {varOne:'show template one', varTwo:'show template two'});
  }

}
```

4. set compoent using ng-template

```html
<ng-container [ngTemplateOutlet]="showTemplate" > </ng-container>

<ng-template #showTemplate >
    <app-testcompo></app-testcompo>
</ng-template>
```

5. use like ng-content.

ng-content not work for for-loops    

> parent.component.html

```html
<app-testcompo>

    <ng-template #testcompo >
        <p>samadhi laksahan</p>
    </ng-template>

</app-testcompo>
```

> child.component.html    

```html
<p >testcompo works!</p>

<ng-container [ngTemplateOutlet]="testCompoRef">
</ng-container>
```

> child.component.ts   

"@ContentChild" usually using for "ng-content" only. But here we are using "@ContentChild"
for "ngTemplate" for get it's ID(#testcompo) from parent component for trick.

```typescript
import { Component, ContentChild, OnInit, TemplateRef } from '@angular/core';

@Component({
  selector: 'app-testcompo',
  templateUrl: './testcompo.component.html',
  styleUrls: ['./testcompo.component.scss']
})
export class TestcompoComponent implements OnInit {

  constructor() { }

  @ContentChild('testcompo', {static:false})  testCompoRef:TemplateRef<any>;

  ngOnInit(): void {
  }
}
```

# get data from api

to create new service
$ ng generate service <service-name>

just think we make service call 'http'

> name.service.ts    

````javascript
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http'; /* add new > line*/

@Injectable({
  providedIn: 'root'
})
export class HttpService {

  constructor(private http:HttpClient) { } /* add new > 'private http:HttpClientModule' */

  myMethod(){  /* add new > fucntion */
      return this.http.get('https://api.openbrewerydb.org/breweries');
  }

}
````

> app.module.ts   

````javascript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { AppComponent } from './app.component';
import { AppRoutingModule } from './/app-routing.module';
import { HomeComponent } from './home/home.component';
import { ProductsComponent } from './products/products.component';

import { HttpClientModule } from '@angular/common/http'; /* add new > line */



@NgModule({
  declarations: [
    AppComponent,
    HomeComponent,
    ProductsComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    HttpClientModule, /* add new > line */
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
````

> home.component.ts  

````javascript
import { Component, OnInit } from '@angular/core';

import { HttpService } from '../http.service' /* add new > line*/

@Component({
  selector: 'app-home',
  templateUrl: './home.component.html',
  styleUrls: ['./home.component.css']
})
export class HomeComponent implements OnInit {

  constructor(private _http:HttpService) { } /* add new > 'private _http:HttpService' */

  ngOnInit(): void {

    this._http.myMethod().subscribe(data=>{ /* add new > function*/
       console.log("api data : ", data);
    });

  }

}

````

# angular deploy with node js

## Proxy To Backend

Using the proxying support in webpack's dev server we can highjack certain URLs and
send them to a backend server. We do this by passing a file to --proxy-config.
for more info you can see[documentation](https://github.com/angular/angular-cli/blob/master/docs/documentation/stories/proxy.md).     

you have to customly create <name>.json file for proxy
``` javascript
{
  "/api": {
    "target": "http://localhost:3000",
    "secure": false
  }
}
```

to run angular using Proxy
```shell
$ ng serve --proxy-config proxy.conf.json
```

store on dist file on <mark>static-folder</mark> or <mark>nginx-server</mark>
```javascript
app.use(express.static(path.join(__dirname,'./dist/my-app/')));
```

use Get respons to send html page .
```javascript
app.get('/',function(req,res){
    return res.sendFile(path.join(__dirname,'./dist/my-app/index.html'));
});
```

# uninstall angular-cli

Using following commands to uninstall :

```shell
npm uninstall -g @angular/cli
npm cache clean --force  // use os admin
```

reinstall angular :

```shell
npm install -g @angular/cli
```
