## 1_Start

Angular is a JavaScript framework to help build a fast SPA web application.

Angular2 (Referred as `Angular`) completely rewrite Angular1 (Referred as `AngularJS`), and got updated as Angular3-7

Angular in end is a JS framework, changing the `DOM` at runtime.

### 1 Download NodeJS, install Angular CLI and create new project
```
npm install -g @angular/cli
ng new project-name
cd project-name
ng serve
```

#### CLI (Command Line Interface)
Takes our code, bundles it up, adds all the angular logic from angular to it, and therefore create a bunch of script files, and inject these scripts into index.html file

#### Install bootstrap: (Optional, used for css)
```
npm install --save bootstrap@3
```
Then go to `angular.json` file, `architect` -> `build` -> `styles`

Add another line: `"node_modules/bootstrap/dist/css/bootstrap.min.css"`
(`styles.css`: a global style sheet)

### 2 How Angular works
`index.html`: The actual single page served by server

`AppComponent`: the root component, write other components in root component

Order: 
- `index.html` is served, contains a bunch of scripts (bundled by CLI)
- Scripts executed
	- `Main.js`: First code to be executed, it will `bootstap(app-module)`, 
	- In `app-module`, from the `bootstrap`, it tells angular that there is a `AppComponent` it should know
	- Then Angular will analyze the app.component.ts, and find the selector `app-root`
- Angular know the `AppComponent`
- With all the information, Angular is able to parse component in `index.html`

