## 3_Databinding

Communication between TS(business logic) and template(HTML)
- TS -> HTML: Output data, like String Interpolation, Property Binding
- HTML -> TS: React to event, like Event Binding

### 1 String Interpolation
```
{{ data }}
{{ function() }}
```
Between the `{{ }}`, you should always return a string.
	
### 2 Property Binding

#### Already exist property or dierective:
```
[property]="variable or function()"   // Bind HTML element property(attribute)
[directive]="variable or function()"  // Bind directives
[variable]="value"    // Pass data to child
```
	
#### Custom property (Data flow from parent to child)

- Parent component
	- `postList` is an array in parent's TS file

- Child component
	- `post` is a variable in child's TS file
	- `@Input()`: All properties of components are **only** accessible inside these component

```
<app-post [post]="let post of postList"></app-post-list> // In parent component

// In the TS file of app-post
@Input() element;
@Input('Alias') element;  // Could use Alias as property name in parent
```

### 3 Event Binding
#### Already built event

`$event`: Will be the data emitted with that event, should be used between `""`. And in the function which `event` is passed in, use `event.target.value` to get the data

```
(event) = "function()"  // event is not the same as html event
(click)="onAddPost($event)"   // Not onClick which is html event
```

#### Custom event (Parent bind child's event)

- Parent component
	- `onPostAdded()` is a function in parent's TS file

- Child component
	- `@Output()`: Output decorator tells angular that this event can be listened to at outside the component
	- The data emitted will be the parameter `$event`

```
<app-post-create (postCreated)="onPostAdded($event)">  // In the parent component

// In the TS file of app-post-create 
@Output() postCreated = new EventEmitter<Type of data>(); 
@Output('Alias') postCreated = new EventEmitter<Type of data>();  // Could use Alias as property name in parent
this.postCreated.emit(post);
```	

### 4 Two way Binding

To use `ngModel`, the `FormsModule` from `@angular/forms` needs to be added in `AppModule`
```
[(ngModel)] = "variable"
```

