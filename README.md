Web Components / Angular Elements

Useful things:
	https://blog.nrwl.io/5-reasons-to-use-angular-elements-390c9a629f89

Video: 'I won't go in details - you have a link on my website with a full description of everything'
		'This video will show you what can be done'
		'The final result will be this view'
Flow: 
	Create one Angular 5 application, one Angular 8 Application, and one React Application.
	Inject them all in a static index.html file and / or inject them all into Angular 5 application.




Joining Files:
`npm install --save-dev concat fs-extra`



STEPS FOR BUILDING A WEB COMPONENT IN ANGULAR
1) In app.module.ts convert bootstrap to entryComponents
2)
 ```export class AppModule {
  constructor(private injector: Injector) {}

  ngDoBootstrap() {
    const el = createCustomElement(AppComponent, {injector: this.injector});
    customElements.define('angular-eight-component', el);
  }
}
```
3) `npm install --save-dev concat fs-extra`
4) In package Json:
`"build:elements": "ng build --prod --output-hashing none && node elements-build.js"`,
5) create elements-build.js in root folder and add this

```
const fs = require('fs-extra');
const concat = require('concat');

(async function build() {
  const files = [
    './dist/Angular8/runtime-es2015.js',
    './dist/Angular8/polyfills-es2015.js',
    './dist/Angular8/main-es2015.js'
  ];

  await fs.ensureDir('elements');
  await concat(files, 'elements/Angular8.js');
  await fs.copyFile(
    './dist/Angular8/styles.css',
    'elements/styles.css'
  );
})();
```

STEPS FOR INTEGRATING A WEBCOMPONENT IN ANGULAR
1) Put the built files in assets of Angular 5 app
2) add   schemas: `[CUSTOM_ELEMENTS_SCHEMA]` to AppModule
3) Do `ng eject`
4) Delete every reference of CommonsChunkPlugin



ISSUE: Loading Webpack 4 in Webpack 2/3 App

https://forum.vuejs.org/t/error-when-loading-vue-on-a-webpage-that-uses-webpack-3/48955

https://stackoverflow.com/questions/39187556/angular-cli-where-is-webpack-config-js-file-new-angular6-does-not-support-ng-e

I had to disable code splitting in vue.config.js and it worked fine

https://github.com/webpack/webpack/issues/8247
https://medium.com/@cliffers/how-to-run-multiple-webpack-instances-on-the-same-page-and-avoid-any-conflicts-4e2fe0f016d1


Do ng eject to eject the webpack.config.js from angular-cli

