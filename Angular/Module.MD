## Module

Angular use Component to build web pages and use Modules to bundle different pieces(like Components) into packages

### Basic

Example code: AppModule
```
import { NgModule } from '@angular/core';

@NgModule({
  declarations: [
    AppComponent,
  ],
  imports: [
    BrowserModule,
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

### Detail
`imports`: add some ohter modules to this module. Angular are split into several modules