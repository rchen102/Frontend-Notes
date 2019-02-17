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

- Already exist property or dierective:
```
[property]="variable or function()"   // Bind HTML element property(attribute)
[directive]="variable or function()"  // Bind directives
[variable]="value"    // Pass data to child
```
	
- Custom property
```
@Input() posts = [];  // In the file of app-post-list
<app-post-list [posts]="storedPosts"> // In the parent component
```

### 3 Event Binding
- Already built event

`$event`: Will be the data emitted with that event, should be used between `""`. And in the function which `event` is passed in, use `event.target.value` to get the data

```
(event) = "function()"  // event is not the same as html event
(click)="onAddPost($event)"   // Not onClick which is html event
```

- Custom event
```
@Output() postCreated = new EventEmitter<Type of data>(); // In the file of app-post-create 
// Output decorator tells angular that this event can be listened to at outside the component
this.postCreated.emit(post);

<app-post-create (postCreated)="onPostAdded($event)">  // In the parent component
```	

### 4 Two way Binding

To use `ngModel`, the `FormsModule` from `@angular/forms` needs to be added in `AppModule`
```
[(ngModel)] = "variable"
```

