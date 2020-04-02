[[_TOC_]]

Note: The following guide has been adapted from the [official Angular Style Guidelines](https://angular.io/guide/styleguide#coding-conventions)

Have a consistent set of coding, naming, and whitespace conventions.

# Classes
**Do** use upper camel case when naming classes.

**Why?** Follows conventional thinking for class names.

**Why?** Classes can be instantiated and construct an instance. By convention, upper camel case indicates a constructable asset.


```ts
app/shared/exception.service.ts
/* avoid */

export class exceptionService {
  constructor() { }
}
```

```ts
//app/shared/exception.service.ts
export class ExceptionService {
  constructor() { }
}
```

# Constants
**Do** declare variables with `const` if their values should not change during the application lifetime.

**Why?** Conveys to readers that the value is invariant.

**Why?** TypeScript helps enforce that intent by requiring immediate initialization and by preventing subsequent re-assignment.

**Consider** spelling `const` variables in lower camel case.

**Why?** Lower camel case variable names (`heroRoutes`) are easier to read and understand than the traditional UPPER_SNAKE_CASE names (`HERO_ROUTES`).

**Why?** The tradition of naming constants in UPPER_SNAKE_CASE reflects an era before the modern IDEs that quickly reveal the `const` declaration. TypeScript prevents accidental reassignment.

**Do** tolerate _existing_ `const` variables that are spelled in UPPER_SNAKE_CASE.

**Why?** The tradition of UPPER_SNAKE_CASE remains popular and pervasive, especially in third party modules. It is rarely worth the effort to change them at the risk of breaking existing code and documentation.

```ts
//app/shared/data.service.ts
export const mockHeroes   = ['Sam', 'Jill']; // prefer
export const heroesUrl    = 'api/heroes';    // prefer
export const VILLAINS_URL = 'api/villains';  // tolerate
```

# Interfaces

**Do** name an interface using upper camel case.

**Consider** naming an interface without an `I` prefix.

**Consider** using a class instead of an interface for services and declarables (components, directives, and pipes).

**Consider** using an interface for data models.

**Why?** <a href="https://github.com/Microsoft/TypeScript/wiki/Coding-guidelines">TypeScript guidelines</a>
discourage the `I` prefix.

**Why?** A class alone is less code than a _class-plus-interface_.

**Why?** A class can act as an interface (use `implements` instead of `extends`).

**Why?** An interface-class can be a provider lookup token in Angular dependency injection.

```ts
//app/shared/hero-collector.service.ts
/* avoid */

import { Injectable } from '@angular/core';

import { IHero } from './hero.model.avoid';

@Injectable()
export class HeroCollectorService {
  hero: IHero;

  constructor() { }
}
```

```ts
//app/shared/hero-collector.service.ts
import { Injectable } from '@angular/core';

import { Hero } from './hero.model';

@Injectable()
export class HeroCollectorService {
  hero: Hero;

  constructor() { }
}
```

# Properties and methods
**Do** use lower camel case to name properties and methods.

**Avoid** prefixing private properties and methods with an underscore.

**Why?** Follows conventional thinking for properties and methods.

**Why?** JavaScript lacks a true private property or method.

**Why?** TypeScript tooling makes it easy to identify private vs. public properties and methods.

```ts
//app/shared/toast.service.ts
/* avoid */

import { Injectable } from '@angular/core';

@Injectable()
export class ToastService {
  message: string;

  private _toastCount: number;

  hide() {
    this._toastCount--;
    this._log();
  }

  show() {
    this._toastCount++;
    this._log();
  }

  private _log() {
    console.log(this.message);
  }
}
```

```ts
//app/shared/toast.service.ts
import { Injectable } from '@angular/core';

@Injectable()
export class ToastService {
  message: string;

  private toastCount: number;

  hide() {
    this.toastCount--;
    this.log();
  }

  show() {
    this.toastCount++;
    this.log();
  }

  private log() {
    console.log(this.message);
  }
}
```

# Import line spacing

**Consider** leaving one empty line between third party imports and application imports.

**Consider** listing import lines alphabetized by the module.

**Consider** listing destructured imported symbols alphabetically.

**Why?** The empty line separates _your_ stuff from _their_ stuff.

**Why?** Alphabetizing makes it easier to read and locate symbols.

```ts
//app/heroes/shared/hero.service.ts
/* avoid */

import { ExceptionService, SpinnerService, ToastService } from '../../core';
import { HttpClient } from '@angular/common/http';
import { Injectable } from '@angular/core';
import { Hero } from './hero.model';
```

```ts
//app/heroes/shared/hero.service.ts
import { HttpClient } from '@angular/common/http';
import { Injectable } from '@angular/core';

import { ExceptionService, SpinnerService, ToastService } from '../../core';
import { Hero } from './hero.model';
```