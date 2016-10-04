Create and Configure Project

##CONFIG FILES NEEDED
	-package.json - npm pack dependencies
	-tsconfig.json - defines how ts compiles to js
	-typings.json - definition files (ts compiler does not natively recognize)
	-systemjs.config.js - info for the module loader - where to find app modules, registers ness. Packs

	-copy/pasted the code for these files in example, but 
		-Learn more about these configuration files in the Npm Package Configuration guide and the TypeScript Configuration guide. A detailed discussion of module loading is beyond the scope of this guide.
		-Although we use SystemJS for illustrative purposes here, it's only one option for loading modules. Use the module loader that you prefer. For Webpack and Angular, seeWebpack: an Introduction. Or, learn more about SystemJS configuration in general here.

	-npm install
		(note, typings may not install properly from the package.json/npm install?)
		(if so, install manually -- npm run typings install)



##CREATE THE APP/MODULE

-angular apps are composed of closely related NgModules
-every app has at least one mod--the root module--entry point of app
	-by convention called AppModule, in file called app.module.ts

-made an app folder
-put an app.module.ts in it, make the module in it

--imports
	-syntax ---- import { THINGY }  from ‘@angular/APIPATH’
	-needs the NgModule - import { NgModule }	from ‘@angular/core’;
	-needs BrowserModule - import { BrowserModule } from ‘@angular/platform-browser’;
		--since it’s a web app, any webapp will need this

--decorate the module
	-syntax --- @NgModule({})
	--give your imports in an array--
		-- imports: [ BrowserModule ]
		-- ...some things from above need imported here, some don’t? XD
		---in a real app, you’d probably import more, like FormsModule, RouterModule, HttpModule

--export your class 
	-- export class AppModule {}
	--i guess the metadata above is implicitly added/related to the class?



##CREATE A COMPONENT

--every angular app has at least one comp, the root component, named AppComponent
--component controls a view --a portion of the screen

--put app.component.ts in app folder

--import Component from angular core
--decorate your component
	@Component({)}
	
	-name selector (html tag) - 	selector: ‘my-app’
	-give template - 		template: ‘<h1>Hi from comp!</h1>’
--export your class
	Export class AppComponent {}



##IMPORT YOUR COMPONENT INTO MODULE

-import at top from ./app.component;  ***note path
-add a declarations array and a bootstrap array, add it to those ****what this do?
declarations: [ AppComponent ],
Bootstrap:  [ AppComponent ]


##START THE APP/BOOTSTRAPPING
-note, bootstrapping apparently is kinda the simple process that will start/run the whole app
-this code will initialize the platform your app rans in and uses the platform to bootstrap your AppModule

-make an app/main.ts

-import platformBrowserDyamic from @angular/platform-browser-dynamic
	--note, this is platform for running in browser
	--for mobile device you might load a module specific to Cordova, etc

-import your app module from ‘./app.module’;
-instantiate the platform --
 const platform = platformBrowserDyamic();
-use the platform’s bootstrapModule method on AppModule
	platform.bootstrapModule(AppModule);


##INDEX.HTML

-link scripts for polyfills for older browsers, and libraries needed by angular
    <!-- Polyfill(s) for older browsers -->
   <script src="node_modules/core-js/client/shim.min.js"></script>

   <script src="node_moduleas/zone.js/dist/zone.js"></script>
   <script src="node_modules/reflect-metadata/Reflect.js"></script>
   <script src="node_modules/systemjs/dist/system.src.js"></script>
-link SystemJS
   <!-- 2. Configure SystemJS -->
   <script src="systemjs.config.js"></script>
-put some js/<script> to import and run the app module (this will refer to the main.js file)
	System.import(‘app’).catch(function(err) {console.error(err); });

-in the body, add your <my-app>Loading…</my-app>

START
	-run npm start
	-package.json sets this up to..
		-put typescript complier in watch mode
		-run static file server lite-server that will load index.html, refreshes browser when app files change

	









