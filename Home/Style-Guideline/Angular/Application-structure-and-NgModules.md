[[_TOC_]]

Note: The following guide has been adapted from the [official Angular Style Guidelines](https://angular.io/guide/styleguide#application-structure-and-ngmodules)

Have a near-term view of implementation and a long-term vision. Start small but keep in mind where the app is heading down the road.

All of the app's code goes in a folder named `src`. All feature areas are in their own folder, with their own NgModule.

All content is one asset per file. Each component, service, and pipe is in its own file. All third party vendor scripts are stored in another folder and not in the `src` folder. You didn't write them and you don't want them cluttering `src`. Use the naming conventions for files in this guide.

# _LIFT_

**Do** structure the app such that you can **L**ocate code quickly, **I**dentify the code at a glance, keep the **F**lattest structure you can, and **T**ry to be DRY.

**Do** define the structure to follow these four basic guidelines, listed in order of importance.

**Why?** LIFT Provides a consistent structure that scales well, is modular, and makes it easier to increase developer efficiency by finding code quickly. To confirm your intuition about a particular structure, ask: _can I quickly open and start work in all of the related files for this feature_?

# Locate

**Do** make locating code intuitive, simple and fast.

**Why?** To work efficiently you must be able to find files quickly, especially when you do not know (or do not remember) the file _names_. Keeping related files near each other in an intuitive location saves time. A descriptive folder structure makes a world of difference to you and the people who come after you.

# Identify

**Do** name the file such that you instantly know what it contains and represents.

**Do** be descriptive with file names and keep the contents of the file to exactly one component.

**Avoid** files with multiple components, multiple services, or a mixture.

**Why?** Spend less time hunting and pecking for code, and become more efficient.
Longer file names are far better than _short-but-obscure_ abbreviated names.

<div class="alert is-helpful">
It may be advantageous to deviate from the _one-thing-per-file_ rule when you have a set of small, closely-related features that are better discovered and understood in a single file than as multiple files. Be wary of this loophole.
</div>

# Flat

**Do** keep a flat folder structure as long as possible.

**Consider** creating sub-folders when a folder reaches seven or more files.

**Consider** configuring the IDE to hide distracting, irrelevant files such as generated `.js` and `.js.map` files.

**Why?** No one wants to search for a file through seven levels of folders.
A flat structure is easy to scan.

On the other hand, <a href="https://en.wikipedia.org/wiki/The_Magical_Number_Seven,_Plus_or_Minus_Two">psychologists believe</a> that humans start to struggle when the number of adjacent interesting things exceeds nine. So when a folder has ten or more files, it may be time to create subfolders.

Base your decision on your comfort level. Use a flatter structure until there is an obvious value to creating a new folder.

# _T-DRY_ (Try to be _DRY_)

**Do** be DRY (Don't Repeat Yourself).

**Avoid** being so DRY that you sacrifice readability.

**Why?** Being DRY is important, but not crucial if it sacrifices the other elements of LIFT. That's why it's called _T-DRY_. For example, it's redundant to name a template `hero-view.component.html` because with the `.html` extension, it is obviously a view. But if something is not obvious or departs from a convention, then spell it out.

# Overall structural guidelines

**Do** start small but keep in mind where the app is heading down the road.

**Do** have a near term view of implementation and a long term vision.

**Do** put all of the app's code in a folder named `src`.

**Do** separate logic when a component gets to large. See the `add-person` example below.

**Consider** creating a folder for a component when it has multiple accompanying files (`.ts`, `.html`, `.css` and `.spec`).

**Why?** Helps keep the app structure small and easy to maintain in the early stages, while being easy to evolve as the app grows.

**Why?** Components often have four files (e.g. `*.html`, `*.css`, `*.ts`, and `*.spec.ts`) and can clutter a folder quickly.

---

Here is a compliant folder and file structure:
Note that this folder structure differs slightly from the Angular official guidelines and is a bit more folder heavy.

![image.png](/.attachments/image-8a1c8b37-0a30-435c-9f47-a35a4d6d7855.png)

<div class="alert is-helpful">
While components in dedicated folders are widely preferred, another option for small apps is to keep components flat (not in a dedicated folder).
This adds up to four files to the existing folder, but also reduces the folder nesting. Whatever you choose, be consistent.
</div>

# _Folders-by-feature_ structure

**Do** create folders named for the feature area they represent.

**Why?** A developer can locate the code and identify what each file represents at a glance. The structure is as flat as it can be and there are no repetitive or redundant names.

**Why?** The LIFT guidelines are all covered.

**Why?** Helps reduce the app from becoming cluttered through organizing the content and keeping them aligned with the LIFT guidelines.

**Why?** When there are a lot of files, for example 10+, locating them is easier with a consistent folder structure and more difficult in a flat structure.

**Do** create an NgModule for each feature area.

**Why?** NgModules make it easy to lazy load routable features.

**Why?** NgModules make it easier to isolate, test, and reuse features.
<a href="#file-tree">Refer to this _folder and file structure_ example.</a>

# App _root module_

**Do** create an NgModule in the app's root folder, for example, in `/src/app`.

**Why?** Every app requires at least one root NgModule.

**Consider** naming the root module `app.module.ts`.

**Why?** Makes it easier to locate and identify the root module.

```ts
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
 
import { AppComponent }    from './app.component';
import { HeroesComponent } from './heroes/heroes.component';
 
@NgModule({
  imports: [
    BrowserModule,
  ],
  declarations: [
    AppComponent,
    HeroesComponent
  ],
  exports: [ AppComponent ],
  entryComponents: [ AppComponent ]
})
export class AppModule {}
```

# Feature modules
**Do** create an NgModule for all distinct features in an application; for example, a `Heroes` feature.

**Do** place the feature module in the same named folder as the feature area; for example, in `app/heroes`.

**Do** name the feature module file reflecting the name of the feature area and folder; for example, `app/heroes/heroes.module.ts`.

**Do** name the feature module symbol reflecting the name of the feature area, folder, and file; for example, `app/heroes/heroes.module.ts` defines `HeroesModule`.

**Why?** A feature module can expose or hide its implementation from other modules.

**Why?** A feature module identifies distinct sets of related components that comprise the feature area.

**Why?** A feature module can easily be routed to both eagerly and lazily.

**Why?** A feature module defines clear boundaries between specific functionality and other application features.

**Why?** A feature module helps clarify and make it easier to assign development responsibilities to different teams.

**Why?** A feature module can easily be isolated for testing.

# Shared feature module
**Do** create a feature module named `SharedModule` in a `shared` folder; for example, `app/shared/shared.module.ts` defines `SharedModule`.

**Do** declare components, directives, and pipes in a shared module when those items will be re-used and referenced by the components declared in other feature modules.

**Consider** using the name SharedModule when the contents of a shared module are referenced across the entire application.

**Consider** <font color="red">_not_</font> providing services in shared modules. Services are usually singletons that are provided once for the entire application or in a particular feature module. There are exceptions, however. For example, in the sample code that follows, notice that the `SharedModule` provides `FilterTextService`. This is acceptable here because the service is stateless;that is, the consumers of the service aren't impacted by new instances.

**Do** import all modules required by the assets in the `SharedModule`; for example, `CommonModule` and `FormsModule`.

**Why?** `SharedModule` will contain components, directives and pipes that may need features from another common module; for example, `ngFor` in `CommonModule`.

**Do** declare all components, directives, and pipes in the `SharedModule`.

**Do** export all symbols from the `SharedModule` that other feature modules need to use.

**Why?** `SharedModule` exists to make commonly used components, directives and pipes available for use in the templates of components in many other modules.

**Avoid** specifying app-wide singleton providers in a `SharedModule`. Intentional singletons are OK. Take care.

**Why?** A lazy loaded feature module that imports that shared module will make its own copy of the service and likely have undesirable results.

**Why?** You don't want each module to have its own separate instance of singleton services. Yet there is a real danger of that happening if the `SharedModule` provides a service.

![2019-02-14_9-40-37.png](/.attachments/2019-02-14_9-40-37-0e1b8066-136b-4e6e-b5d4-93faaad16e22.png)

```ts
//app/shared/shared.module.ts
import { NgModule }      from '@angular/core';
import { CommonModule }  from '@angular/common';
import { FormsModule }   from '@angular/forms';

import { FilterTextComponent } from './filter-text/filter-text.component';
import { FilterTextService }   from './filter-text/filter-text.service';
import { InitCapsPipe }        from './init-caps.pipe';

@NgModule({
  imports: [CommonModule, FormsModule],
  declarations: [
    FilterTextComponent,
    InitCapsPipe
  ],
  providers: [FilterTextService],
  exports: [
    CommonModule,
    FormsModule,
    FilterTextComponent,
    InitCapsPipe
  ]
})
export class SharedModule { }
```

```ts
//app/shared/init-caps.pipe.ts
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({ name: 'initCaps' })
export class InitCapsPipe implements PipeTransform {
  transform = (value: string) => value;
}
```

```ts
//app/shared/filter-text/filter-text.component.ts
import { Injectable } from '@angular/core';

@Injectable()
export class FilterTextService {
  constructor() {
    console.log('Created an instance of FilterTextService');
  }

  filter(data: string, props: Array<string>, originalList: Array<any>) {
    let filteredList: any[];
    if (data && props && originalList) {
      data = data.toLowerCase();
      let filtered = originalList.filter(item => {
        let match = false;
        for (let prop of props) {
          if (item[prop].toString().toLowerCase().indexOf(data) > -1) {
            match = true;
            break;
          }
        };
        return match;
      });
      filteredList = filtered;
    } else {
      filteredList = originalList;
    }
    return filteredList;
  }
}
```

```ts
//app/heroes/heroes.component.ts
import { Component } from '@angular/core';

import { FilterTextService } from '../shared/filter-text/filter-text.service';

@Component({
  selector: 'toh-heroes',
  templateUrl: './heroes.component.html'
})
export class HeroesComponent {

  heroes = [
    { id: 1, name: 'Windstorm' },
    { id: 2, name: 'Bombasto' },
    { id: 3, name: 'Magneta' },
    { id: 4, name: 'Tornado' }
  ];

  filteredHeroes = this.heroes;

  constructor(private filterService: FilterTextService) { }

  filterChanged(searchText: string) {
    this.filteredHeroes = this.filterService.filter(searchText, ['id', 'name'], this.heroes);
  }
}
```

```html
<!-- app/heroes/heroes.component.html -->
<div>This is heroes component</div>
<ul>
  <li *ngFor="let hero of filteredHeroes">
    {{hero.name}}
  </li>
</ul>
<toh-filter-text (changed)="filterChanged($event)"></toh-filter-text>
```

# Core feature module
**Consider** collecting numerous, auxiliary, single-use classes inside a core module to simplify the apparent structure of a feature module.
**Consider** calling the application-wide core module, `CoreModule`. Importing `CoreModule` into the root `AppModule` reduces its complexity and emphasizes its role as orchestrator of the application as a whole.

**Do** create a feature module named `CoreModule` in a `core` folder (e.g. `app/core/core.module.ts` defines `CoreModule`).

**Do** put a singleton service whose instance will be shared throughout the application in the `CoreModule` (e.g. `ExceptionService` and `LoggerService`).

**Do** import all modules required by the assets in the `CoreModule` (e.g. `CommonModule` and `FormsModule`).

**Why?** `CoreModule` provides one or more singleton services. Angular registers the providers with the app root injector, making a singleton instance of each service available to any component that needs them, whether that component is eagerly or lazily loaded.

**Why?** `CoreModule` will contain singleton services. When a lazy loaded module imports these, it will get a new instance and not the intended app-wide singleton.

**Do** gather application-wide, single use components in the `CoreModule`. Import it once (in the `AppModule`) when the app starts and never import it anywhere else. (e.g. `NavComponent` and `SpinnerComponent`).

**Why?** Real world apps can have several single-use components (e.g., spinners, message toasts, and modal dialogs) that appear only in the `AppComponent` template. They are not imported elsewhere so they're not shared in that sense. Yet they're too big and messy to leave loose in the root folder.

**Avoid** importing the `CoreModule` anywhere except in the `AppModule`.

**Why?** A lazily loaded feature module that directly imports the `CoreModule` will make its own copy of services and likely have undesirable results.

**Why?** An eagerly loaded feature module already has access to the `AppModule`'s injector, and thus the `CoreModule`'s services.

**Do** export all symbols from the `CoreModule` that the `AppModule` will import and make available for other feature modules to use.

**Why?** `CoreModule` exists to make commonly used singleton services available for use in the many other modules.

**Why?** You want the entire app to use the one, singleton instance. You don't want each module to have its own separate instance of singleton services. Yet there is a real danger of that happening accidentally if the `CoreModule` provides a service.

![2019-02-14_9-33-12.png](/.attachments/2019-02-14_9-33-12-b9a138fa-b5db-4bb2-ab90-40ab54ff85ea.png)

```ts
//app/app.module.ts
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

import { AppComponent }   from './app.component';
import { HeroesComponent } from './heroes/heroes.component';
import { CoreModule }    from './core/core.module';

@NgModule({
  imports: [
    BrowserModule,
    CoreModule,
  ],
  declarations: [
    AppComponent,
    HeroesComponent
  ],
  exports: [ AppComponent ],
  entryComponents: [ AppComponent ]
})
export class AppModule {}
```

```ts
//app/core/core.module.ts
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';

import { LoggerService } from './logger.service';
import { NavComponent } from './nav/nav.component';
import { SpinnerComponent } from './spinner/spinner.component';
import { SpinnerService } from './spinner/spinner.service';

@NgModule({
  imports: [
    CommonModule // we use ngFor
  ],
  exports: [NavComponent, SpinnerComponent],
  declarations: [NavComponent, SpinnerComponent],
  providers: [LoggerService, SpinnerService]
})
export class CoreModule { }
```

```ts
//app/core/logger.service.ts
import { Injectable } from '@angular/core';

@Injectable()
export class LoggerService {
  log(msg: string) {
    console.log(msg);
  }

  error(msg: string) {
    console.error(msg);
  }
}
```

```ts
//app/core/nav/nav.component.ts
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'toh-nav',
  templateUrl: './nav.component.html',
  styleUrls: ['./nav.component.css'],
})
export class NavComponent implements OnInit {
  menuItems = [
    'Heroes',
    'Villains',
    'Other'
  ];

  ngOnInit() {  }

  constructor() { }
}
```
```
<!-- app/core/nav/nav.component.html -->
<header>
  <div>
    <h4>Tour of Heroes</h4>
  </div>
  <nav>
    <ul>
      <li *ngFor="let item of menuItems">
        {{item}}
      </li>
    </ul>
  </nav>
  <br/>
</header>
```
```ts
//app/core/spinner/spinner.component.ts
import { Component, OnDestroy, OnInit } from '@angular/core';
import { Subscription } from 'rxjs';

import { LoggerService } from '../logger.service';
import { SpinnerState, SpinnerService } from './spinner.service';

@Component({
  selector: 'toh-spinner',
  templateUrl: './spinner.component.html',
  styleUrls: ['./spinner.component.css']
})
export class SpinnerComponent implements OnDestroy, OnInit {
  visible = false;

  private spinnerStateChanged: Subscription;

  constructor(
    private loggerService: LoggerService,
    private spinnerService: SpinnerService
  ) { }

  ngOnInit() {
    console.log(this.visible);
    this.spinnerStateChanged = this.spinnerService.spinnerState
      .subscribe((state: SpinnerState) => {
        this.visible = state.show;
        this.loggerService.log(`visible=${this.visible}`);
      });
  }

  ngOnDestroy() {
    this.spinnerStateChanged.unsubscribe();
  }
}
```

```
<!-- app/core/spinner/spinner.component.html -->
<div class="spinner" [class.spinner-hidden]="!visible"> </div>
```

```ts
//app/core/spinner/spinner.service.ts
import { Injectable } from '@angular/core';
import { Subject } from 'rxjs';

export interface SpinnerState {
  show: boolean;
}

@Injectable()
export class SpinnerService {
  private spinnerSubject = new Subject<SpinnerState>();

  spinnerState = this.spinnerSubject.asObservable();

  constructor() { }

  show() {
    this.spinnerSubject.next(<SpinnerState>{ show: true });
  }

  hide() {
    this.spinnerSubject.next(<SpinnerState>{ show: false });
  }
}
```

<div class="alert is-helpful">
`AppModule` is a little smaller because many app/root classes have moved to other modules. `AppModule` is stable because you will add future components and providers to other modules, not this one. `AppModule` delegates to imported modules rather than doing work. `AppModule` is focused on its main task, orchestrating the app as a whole.
</div>

# Prevent re-import of the core module

**Do** guard against reimporting of `CoreModule` and fail fast by adding guard logic.

**Why?** Guards against reimporting of the `CoreModule`.

**Why?** Guards against creating multiple instances of assets intended to be singletons.

```ts
//app/core/module-import-guard.ts
export function throwIfAlreadyLoaded(parentModule: any, moduleName: string) {
  if (parentModule) {
    throw new Error(`${moduleName} has already been loaded. Import Core modules in the AppModule only.`);
  }
}
```

```ts
//app/core/core.module.ts
import { NgModule, Optional, SkipSelf } from '@angular/core';
import { CommonModule } from '@angular/common';

import { LoggerService } from './logger.service';
import { NavComponent } from './nav/nav.component';
import { throwIfAlreadyLoaded } from './module-import-guard';

@NgModule({
  imports: [
    CommonModule // we use ngFor
  ],
  exports: [NavComponent],
  declarations: [NavComponent],
  providers: [LoggerService]
})
export class CoreModule {
  constructor( @Optional() @SkipSelf() parentModule: CoreModule) {
    throwIfAlreadyLoaded(parentModule, 'CoreModule');
  }
}
```

# Lazy Loaded folders

**Do** put the contents of lazy loaded features in a *lazy loaded folder*. A typical *lazy loaded folder* contains a *routing component*, its child components, and their related assets and modules.

**Why?** The folder makes it easy to identify and isolate the feature content.

# Never directly import lazy loaded folders

**Avoid** allowing modules in sibling and parent folders to directly import a module in a *lazy loaded feature*.

**Why?** Directly importing and using a module will load it immediately when the intention is to load it on demand.