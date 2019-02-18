## 4_Directive

Directives are instructions you place in the DOM

- Directives with a template
- Directives without template

Components are kind of directives with template.


### Structural Directives

Directives that will change the DOM

#### `*ngIf`: conditional add or remove html elements from DOM 

```
<p *ngIf="LikeU; else DoNotLikeU">Hello</p>
<ng-template #DoNotLikeU> // Could also add else, # is local reference
	<p></p>
</ng-template>
```
Between the `""`, you should put or return a boolean

#### `*ngFor`: loop through all elements 

```
<post *ngFor="let item of posts; let i = index"></post>
```

### Attribute Directives

Directives that do not change the DOM, onli change the element where they are

The name is due to it just looks like normal HTML attributes.

#### `ngStyle`: use property binding to dynamically change style

```
<p [ngStyle]="{backgroundColor: getColor()}">Hello</p>  // Use camel case or 'background-color' to be a valid JS property name
```
Between the `""`, you should put a JS object {styleName: styleValue}

#### `ngClass`: use property binding to dynamically add or remove css classes

```
<p [ngClass]="{}">Hello</p>
```
Between the `""`, you should put a JS object {className: boolean}
