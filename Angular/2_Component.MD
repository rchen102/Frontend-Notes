## 2_Component

Angular thinks in Components, build whole app by composing it from a couple of Components

Pros: Allow us to split complex app into reusable part. Easily to maintain and manage.

### 1 Bsice
```
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
}
```
Each component has its own template(`html`), its own business logic(`ts`) and style(`css`)

### 2 Explanation
