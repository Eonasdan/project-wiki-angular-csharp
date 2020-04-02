Naming conventions are hugely important to maintainability and readability. This guide recommends naming conventions for the file name and the symbol name.

[[_TOC_]]

Note: The following guide has been adapted from the [official Angular Style Guidelines](https://angular.io/guide/styleguide#naming)

# General Naming Guidelines

**Do** use consistent names for all symbols.

**Do** follow a pattern that describes the symbol's feature then its type. The recommended pattern is `feature.type.ts`.

**Why?** Naming conventions help provide a consistent way to find content at a glance. Consistency within the project is vital. Consistency with a team is important. Consistency across a company provides tremendous efficiency.

**Why?** The naming conventions should simply help find desired code faster and make it easier to understand.

**Why?** Names of folders and files should clearly convey their intent. For example, `app/heroes/hero-list.component.ts` may contain a component that manages a list of heroes.

# Separate file names with dots and dashes

**Do** use lowercase file names.

**Do** use dashes to separate words in the descriptive name.

**Do** use dots to separate the descriptive name from the type.

**Do** use consistent type names for all components following a pattern that describes the **Do** use conventional type names including `.service`, `.component`, `.pipe`, `.module`, and `.directive`. Invent additional type names if you must but take care not to create too many.

**Why?** Type names provide a consistent way to quickly identify what is in the file.

**Why?** Type names make it easy to find a specific file type using an editor or IDE's fuzzy search techniques.

**Why?** Unabbreviated type names such as `.service` are descriptive and unambiguous. Abbreviations such as `.srv`, `.svc`, and `.serv` can be confusing.

**Why?** Type names provide pattern matching for any automated tasks.

# Symbols and file names

**Do** use consistent names for all assets named after what they represent.

**Do** use upper camel case for class names.

**Do** match the name of the symbol to the name of the file.

**Do** append the symbol name with the conventional suffix (such as `Component`, `Directive`, `Module`, `Pipe`, or `Service`) for a thing of that type.

**Do** give the filename the conventional suffix (such as `.component.ts`, `.directive.ts`, `.module.ts`, `.pipe.ts`, or `.service.ts`) for a file of that type.

**Why?** Consistent conventions make it easy to quickly identify and reference assets of different types.

|Symbol Name|File Name|
|--- |--- |
|@Component({ ... })<br/>export class AppComponent { }|app.component.ts|
|@Component({ ... })<br/>export class HeroesComponent { }|heroes.component.ts|
|@Component({ ... })<br/>export class HeroListComponent { }|hero-list.component.ts|
|@Component({ ... })<br/>export class HeroDetailComponent { }|hero-detail.component.ts|
|@Directive({ ... })<br/>export class ValidationDirective { }|validation.directive.ts|
|@NgModule({ ... })<br/>export class AppModule|app.module.ts|
|@Pipe({ name: 'initCaps' })<br/>export class InitCapsPipe implements PipeTransform { }|init-caps.pipe.ts|
|@Injectable()<br/>export class UserProfileService { }|user-profile.service.ts|

# Service names

**Do** use consistent names for all services named after their feature.

**Do** suffix a service class name with `Service`. For example, something that gets data or heroes should be called a `DataService` or a `HeroService`.

A few terms are unambiguously services. They typically indicate agency by ending in "-er". You may prefer to name a service that logs messages `Logger` rather than `LoggerService`. Decide if this exception is agreeable in your project. As always, strive for consistency.

**Why?** Provides a consistent way to quickly identify and reference services.

**Why?** Clear service names such as `Logger` do not require a suffix.

**Why?** Service names such as `Credit` are nouns and require a suffix and should be named with a suffix when it is not obvious if it is a service or something else.

|Symbol Name|File Name|
|--- |--- |
|@Injectable()<br/>export class HeroDataService { }|hero-data.service.ts|
|@Injectable()<br/>export class CreditService { }|credit.service.ts|
|@Injectable()<br/>export class Logger { }|logger.service.ts|

# Bootstrapping

**Do** put bootstrapping and platform logic for the app in a file named `main.ts`.

**Do** include error handling in the bootstrapping logic.

**Avoid** putting app logic in `main.ts`. Instead, consider placing it in a component or service.

**Why?** Follows a consistent convention for the startup logic of an app.

**Why?** Follows a familiar convention from other technology platforms.

```ts
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';

import { AppModule } from './app/app.module';

platformBrowserDynamic().bootstrapModule(AppModule)
  .then(success => console.log(`Bootstrap success`))
  .catch(err => console.error(err));
```

# Component selectors

**Do** use _dashed-case_ or _kebab-case_ for naming the element selectors of components.

**Why?** Keeps the element names consistent with the specification for [Custom Elements](https://www.w3.org/TR/custom-elements/).

<font color="red">*Don't do this*.</font>
```ts
/* avoid */

@Component({
  selector: 'tohHeroButton',
  templateUrl: './hero-button.component.html'
})
export class HeroButtonComponent {}
```

```ts
//app/heroes/shared/hero-button/hero-button.component.ts
@Component({
  selector: 'toh-hero-button',
  templateUrl: './hero-button.component.html'
})
export class HeroButtonComponent {}
```

```ts
//app/app.component.html
<toh-hero-button></toh-hero-button>
```

# Component custom prefix
**Do** use a hyphenated, lowercase element selector value (e.g. `admin-users`).

**Do** use a custom prefix for a component selector. For example, the prefix `toh` represents from **T**our **o**f **H**eroes and the prefix `admin` represents an admin feature area.

**Do** use a prefix that identifies the feature area or the app itself.

**Why?** Prevents element name collisions with components in other apps and with native HTML elements.

**Why?** Makes it easier to promote and share the component in other apps.

**Why?** Components are easy to identify in the DOM.

<font color="red">*Don't do this*.</font>
```ts
/* avoid */

// HeroComponent is in the Tour of Heroes feature
@Component({
  selector: 'hero'
})
export class HeroComponent {}
```

<font color="red">*Don't do this*.</font>
```ts
/* avoid */

// UsersComponent is in an Admin feature
@Component({
  selector: 'users'
})
export class UsersComponent {}
```

```ts
//app/heroes/hero.component.ts
@Component({
  selector: 'toh-hero'
})
export class HeroComponent {}
```

```ts
//app/users/users.component.ts
@Component({
  selector: 'admin-users'
})
export class UsersComponent {}
```

# Directive selectors
**Do** Use lower camel case for naming the selectors of directives.

**Why?** Keeps the names of the properties defined in the directives that are bound to the view consistent with the attribute names.

**Why?** The Angular HTML parser is case sensitive and recognizes lower camel case.

# Directive custom prefix
**Do** use a custom prefix for the selector of directives (e.g, the prefix `toh` from **T**our **o**f **H**eroes).

**Do** spell non-element selectors in lower camel case unless the selector is meant to match a native HTML attribute.

**Why?** Prevents name collisions.

**Why?** Directives are easily identified.

<font color="red">*Don't do this*.</font>
```ts
/* avoid */

@Directive({
  selector: '[validate]'
})
export class ValidateDirective {}
```

---

```ts
//app/shared/validate.directive.ts
@Directive({
  selector: '[tohValidate]'
})
export class ValidateDirective {}
```

# Pipe names
**Do** use consistent names for all pipes, named after their feature.

**Why?** Provides a consistent way to quickly identify and reference pipes.


<table width="100%">
  <tr>
    <th>
      Symbol Name
    </th>
    <th>
      File Name
    </th>
  </tr>
  <tr style=top>
    <td>
        @Pipe({ name: 'ellipsis' })<br/>
        export class EllipsisPipe implements PipeTransform { }
    </td>
    <td>
      ellipsis.pipe.ts
    </td>
  </tr>
  <tr style=top>
    <td>
        @Pipe({ name: 'initCaps' })<br/>
        export class InitCapsPipe implements PipeTransform { }
    </td>
    <td>
      init-caps.pipe.ts
    </td>
  </tr>
</table>

# Unit test file names

**Do** name test specification files the same as the component they test.

**Do** name test specification files with a suffix of `.spec`.

**Why?** Provides a consistent way to quickly identify tests.

**Why?** Provides pattern matching for [karma](http://karma-runner.github.io/) or other test runners.

<table width="100%">
  <tr>
    <th>
      Test Type
    </th>
    <th>
      File Names
    </th>
  </tr>
  <tr style=top>
    <td>
      Components
    </td>
    <td>
      heroes.component.spec.ts<br/>
      hero-list.component.spec.ts<br/>
      hero-detail.component.spec.ts
    </td>
  </tr>
  <tr style=top>
    <td>
      Services
    </td>
    <td>
      logger.service.spec.ts<br/>
      hero.service.spec.ts<br/>
      filter-text.service.spec.ts
    </td>
  </tr>
  <tr style=top>
    <td>
      Pipes
    </td>
    <td>
      ellipsis.pipe.spec.ts<br/>
      init-caps.pipe.spec.ts
    </td>
  </tr>
</table>

# _End-to-End_ (E2E) test file names
**Do** name end-to-end test specification files after the feature they test with a suffix of `.e2e-spec`.

**Why?** Provides a consistent way to quickly identify end-to-end tests.

**Why?** Provides pattern matching for test runners and build automation.

<table width="100%">
  <tr>
    <th>
      Test Type
    </th>
    <th>
      File Names
    </th>
  </tr>
  <tr style=top>
    <td>
      End-to-End Tests
    </td>
    <td>
      app.e2e-spec.ts<br/>
      heroes.e2e-spec.ts
    </td>
  </tr>
</table>

# Angular _NgModule_ names

**Do** append the symbol name with the suffix `Module`.

**Do** give the file name the `.module.ts` extension.

**Do** name the module after the feature and folder it resides in.

**Why?** Provides a consistent way to quickly identify and reference modules.

**Why?** Upper camel case is conventional for identifying objects that can be instantiated using a constructor.

**Why?** Easily identifies the module as the root of the same named feature.

**Do** suffix a _RoutingModule_ class name with `RoutingModule`.

**Do** end the filename of a _RoutingModule_ with `-routing.module.ts`.

**Why?** A `RoutingModule` is a module dedicated exclusively to configuring the Angular router. A consistent class and file name convention make these modules easy to spot and verify.

<table width="100%">
  <tr>
    <th>
      Symbol Name
    </th>
    <th>
      File Name
    </th>
  </tr>
  <tr style=top>
    <td>
        @NgModule({ ... })<br/>
        export class AppModule { }
    </td>
    <td>
      app.module.ts
    </td>
  </tr>
 <tr style=top>
    <td>
        @NgModule({ ... })<br/>
        export class HeroesModule { }
    </td>
    <td>
      heroes.module.ts
    </td>
  </tr>
  <tr style=top>
    <td>
        @NgModule({ ... })<br/>
        export class VillainsModule { }
    </td>
    <td>
      villains.module.ts
    </td>
  </tr>
  <tr style=top>
    <td>
        @NgModule({ ... })<br/>
        export class AppRoutingModule { }
    </td>
    <td>
      app-routing.module.ts
    </td>
  </tr>
  <tr style=top>
    <td>
        @NgModule({ ... })<br/>
        export class HeroesRoutingModule { }
    </td>
    <td>
      heroes-routing.module.ts
    </td>
  </tr>
</table>