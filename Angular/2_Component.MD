## 2_Component

Angular thinks in Components, build whole app by composing it from a couple of Components

Pros: Allow us to split complex app into reusable part. (Separate business logic, style)

Easily to maintain and manage

### 1 Basic

Create a Component:
```
ng g c name
ng g c name --spec false // without test file
```

Example code: 
```
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',    // Should be Unique
  templateUrl: './app.component.html',  // can use inline html 
  styleUrls: ['./app.component.css']    // can use inline css 
})
export class AppComponent {
}
```

Each component has its own template(`html`), its own business logic(`ts`) and style(`css`)

Decorator: `@Component()` To mark it as a component. Pass a JS Object to configure it



Before use a component, we will have to register it in a module so that Angular know this component exists. Register it in the `declarations` 

### 2 Enhanced

#### (1) selector: 
- It actuall works like css selector, we could select by
- Element: `selector: 'app-root'`
- Attribute: `selector: '[app-root]'` => the component wil become a directive with a template
- Class: `selector: '.app-root'` (Does not work by ID and pseudo selectors)

#### (2) styleUrls: 
- Angular enforece Encapsulating styles for the component they belong to
- We could add `encapsulation: ViewEncapsulation.None` to disable the encapsulating
- `encapsulation: ViewEncapsulation.Native` for browser supports shadow DOM, should work as same as emulated
- Emulate shadow DOM: Using **attribute selector**, give each element a unique atttribute


#### (3) local reference:
- How to use: `#` + `anyname`, and put it at any HTML element, it will hold a reference to the element
- Only could be used anywhere in the template(HTML). Outside like TS file, you could not use it
- Take care: **should not** change element through local reference, Angular has a better way to access DOM, like directives

```
<input type="text" #nameInput>
<button (click)="onAddMember(nameInput)"></button>  // Pass the local reference to the TS file

// In TS file
console.log(nameInput); // return a whole element, like <input type="text" class="xxx">
console.log(nameInput.value); // return the name, like 'xiaomin'
```

#### (4) @ViewChild()
- Using localreference, we can get access to element when method is called, but we also want to get reference before method call
- `@ViewChild(selctor)`: we should pass a selctor 
	- It can be a localreference, should pass as a string
	- It can be a Component Type
- Take care: **should not** change element through local reference, Angular has a better way to access DOM, like directives

```
<input type="text" #nameInput>

// In TS file
@ViewChild('nameInput') nameInputContent: ElementRef;
console.log(nameInputContent); // Type: ElementRef
console.log(nameInputContent.nativeElement.value); // return the name, like 'xiaomin'
```

#### (5) ng-content

- Background: Everything between your own component tag will be lost by default. 
- `ng-content` could solve this problem, project content into components

```
<app-list><p>Without ng-content, the message will get lost</p></app-list> // Project content into app-list

// In <app-list> component HTML file
<div>
	<ng-content></ng-content>  // It will be replaced by <p>xxxx</p>
</div>
```



