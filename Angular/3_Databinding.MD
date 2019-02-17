## 3_Databinding

Communication between TS(business logic) and template(HTML)
- TS -> HTML: Output data, like String Interpolation, Property Binding
- HTML -> TS: React to event, like Event Binding

### 1 String Interpolation

```
{{ data }}
```
	
### 2 Property Binding

- Already exist property:
```
[property] = "data"
[value]="data"
```
	
- Custom property
```
@Input() posts = [];  // In the file of app-post-list
<app-post-list [posts]="storedPosts"> // In the parent component
```

### 3 Event Binding
- Already built event
```
(event) = "function()"  // event is not the same as html event
(click)="onAddPost()"
```
- Custom event
```
@Output() postCreated = new EventEmitter<Type of data>(); // In the file of app-post-create 
// Output decorator tells angular that this event can be listened to at outside the component
this.postCreated.emit(post);

<app-post-create (postCreated)="onPostAdded($event)">  // In the parent component
```	

### 4 Two way Binding
```
[(ngModel)] = "data"
```

