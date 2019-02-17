## 2_Component

Angular thinks in Components, build whole app by composing it from a couple of Components

Pros: Allow us to split complex app into reusable part. (Separate business logic, style)

Easily to maintain and manage

### 1 Basic

Create a Component:
```
ng g c name
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

### 2 Explanation

Each component has its own template(`html`), its own business logic(`ts`) and style(`css`)

Decorator: `@Component()` To mark it as a component. Pass a JS Object to configure it

Selector: it actuall works like css selector, we could select by
- Element: `selector: 'app-root'`
- Attribute: `selector: '[app-root]'`
- Class: `selector: '.app-root'` (Do not work by ID and pseudo selectors)

Before use a component, we will have to register it in a module so that Angular know this component exists. Register it in the `declarations` 


