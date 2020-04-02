[[_TOC_]]

Note: The following guide has been adapted from the [official Angular Style Guidelines](https://angular.io/guide/styleguide#components)

# Components as elements

**Consider** giving components an _element_ selector, as opposed to _attribute_ or _class_ selectors.

**Why?** components have templates containing HTML and optional Angular template syntax. They display content. Developers place components on the page as they would native HTML elements and web components.

**Why?** It is easier to recognize that a symbol is a component by looking at the template's html.

<div class="alert is-helpful">

There are a few cases where you give a component an attribute, such as when you want to augment a built-in element. For example, [Material Design](https://material.angular.io/components/button/overview) uses this technique with `<button mat-button>`. However, you wouldn't use this technique on a custom element.
</div>

```
//app/heroes/hero-button/hero-button.component.ts
/* avoid */

@Component({
  selector: '[tohHeroButton]',
  templateUrl: './hero-button.component.html'
})
export class HeroButtonComponent {}
```
```
<!-- avoid - app/app.component.html -->

<div tohHeroButton></div>
```
---

```
//app/heroes/shared/hero-button/hero-button.component.ts
@Component({
  selector: 'toh-hero-button',
  templateUrl: './hero-button.component.html'
})
export class HeroButtonComponent {}
```
```
<!-- app/app.component.html -->
<toh-hero-button></toh-hero-button>
```

# Extract templates and styles to their own files

**Do** extract templates and styles into a separate file, when more than 3 lines.

**Do** name the template file `[component-name].component.html`, where [component-name] is the component name.

**Do** name the style file `[component-name].component.css`, where [component-name] is the component name.

**Do** specify _component-relative_ URLs, prefixed with `./`.

**Why?** Large, inline templates and styles obscure the component's purpose and implementation, reducing readability and maintainability.

**Why?** In most editors, syntax hints and code snippets aren't available when developing inline templates and styles. The Angular TypeScript Language Service (forthcoming) promises to overcome this deficiency for HTML templates in those editors that support it; it won't help with CSS styles.

**Why?** A _component relative_ URL requires no change when you move the component files, as long as the files stay together.

**Why?** The `./` prefix is standard syntax for relative URLs; don't depend on Angular's current ability to do without that prefix.


```
//app/heroes/heroes.component.ts
/* avoid */

@Component({
  selector: 'toh-heroes',
  template: `
    <div>
      <h2>My Heroes</h2>
      <ul class="heroes">
        <li *ngFor="let hero of heroes | async" (click)="selectedHero=hero">
          <span class="badge">{{hero.id}}</span> {{hero.name}}
        </li>
      </ul>
      <div *ngIf="selectedHero">
        <h2>{{selectedHero.name | uppercase}} is my hero</h2>
      </div>
    </div>
  `,
  styles: [`
    .heroes {
      margin: 0 0 2em 0;
      list-style-type: none;
      padding: 0;
      width: 15em;
    }
    .heroes li {
      cursor: pointer;
      position: relative;
      left: 0;
      background-color: #EEE;
      margin: .5em;
      padding: .3em 0;
      height: 1.6em;
      border-radius: 4px;
    }
    .heroes .badge {
      display: inline-block;
      font-size: small;
      color: white;
      padding: 0.8em 0.7em 0 0.7em;
      background-color: #607D8B;
      line-height: 1em;
      position: relative;
      left: -1px;
      top: -4px;
      height: 1.8em;
      margin-right: .8em;
      border-radius: 4px 0 0 4px;
    }
  `]
})
export class HeroesComponent implements OnInit {
  heroes: Observable<Hero[]>;
  selectedHero: Hero;

 constructor(private heroService: HeroService) { }

  ngOnInit() {
    this.heroes = this.heroService.getHeroes();
  }
}
```

---

```
//app/heroes/heroes.component.ts
@Component({
  selector: 'toh-heroes',
  templateUrl: './heroes.component.html',
  styleUrls:  ['./heroes.component.css']
})
export class HeroesComponent implements OnInit {
  heroes: Observable<Hero[]>;
  selectedHero: Hero;

 constructor(private heroService: HeroService) { }

  ngOnInit() {
    this.heroes = this.heroService.getHeroes();
  }
}
```
```
<!-- app/heroes/heroes.component.html -->
<div>
  <h2>My Heroes</h2>
  <ul class="heroes">
    <li *ngFor="let hero of heroes | async" (click)="selectedHero=hero">
      <span class="badge">{{hero.id}}</span> {{hero.name}}
    </li>
  </ul>
  <div *ngIf="selectedHero">
    <h2>{{selectedHero.name | uppercase}} is my hero</h2>
  </div>
</div>
```
```css
/* app/heroes/heroes.component.css */
.heroes {
  margin: 0 0 2em 0;
  list-style-type: none;
  padding: 0;
  width: 15em;
}
.heroes li {
  cursor: pointer;
  position: relative;
  left: 0;
  background-color: #EEE;
  margin: .5em;
  padding: .3em 0;
  height: 1.6em;
  border-radius: 4px;
}
.heroes .badge {
  display: inline-block;
  font-size: small;
  color: white;
  padding: 0.8em 0.7em 0 0.7em;
  background-color: #607D8B;
  line-height: 1em;
  position: relative;
  left: -1px;
  top: -4px;
  height: 1.8em;
  margin-right: .8em;
  border-radius: 4px 0 0 4px;
}
```

# Decorate _input_ and _output_ properties

**Do** use the `@Input()` and `@Output()` class decorators instead of the `inputs` and `outputs` properties of the
`@Directive` and `@Component` metadata:

**Consider** placing `@Input()` or `@Output()` on the same line as the property it decorates.

**Why?** It is easier and more readable to identify which properties in a class are inputs or outputs.

**Why?** If you ever need to rename the property or event name associated with `@Input` or `@Output`, you can modify it in a single place.

**Why?** The metadata declaration attached to the directive is shorter and thus more readable.

**Why?** Placing the decorator on the same line _usually_ makes for shorter code and still easily identifies the property as an input or output.
Put it on the line above when doing so is clearly more readable.

```
//app/heroes/shared/hero-button/hero-button.component.ts
/* avoid */

@Component({
  selector: 'toh-hero-button',
  template: `<button></button>`,
  inputs: [
    'label'
  ],
  outputs: [
    'change'
  ]
})
export class HeroButtonComponent {
  change = new EventEmitter<any>();
  label: string;
}
```

```
//app/heroes/shared/hero-button/hero-button.component.ts
@Component({
  selector: 'toh-hero-button',
  template: `<button>{{label}}</button>`
})
export class HeroButtonComponent {
  @Output() change = new EventEmitter<any>();
  @Input() label: string;
}
```

# Avoid aliasing _inputs_ and _outputs_

**Avoid** _input_ and _output_ aliases except when it serves an important purpose.

**Why?** Two names for the same property (one private, one public) is inherently confusing.

**Why?** You should use an alias when the directive name is also an _input_ property, and the directive name doesn't describe the property.

```
//app/heroes/shared/hero-button/hero-button.component.ts
/* avoid pointless aliasing */

@Component({
  selector: 'toh-hero-button',
  template: `<button>{{label}}</button>`
})
export class HeroButtonComponent {
  // Pointless aliases
  @Output('changeEvent') change = new EventEmitter<any>();
  @Input('labelAttribute') label: string;
}
```
```
<!-- app/app.component.html -->
<!-- avoid -->

<toh-hero-button labelAttribute="OK" (changeEvent)="doSomething()">
</toh-hero-button>
```

---

```
//app/heroes/shared/hero-button/hero-button.component.ts
@Component({
  selector: 'toh-hero-button',
  template: `<button>{{label}}</button>`
})
export class HeroButtonComponent {
  // No aliases
  @Output() change = new EventEmitter<any>();
  @Input() label: string;
}
```

```
//app/heroes/shared/hero-button/hero-highlight.directive.ts
import { Directive, ElementRef, Input, OnChanges } from '@angular/core';

@Directive({ selector: '[heroHighlight]' })
export class HeroHighlightDirective implements OnChanges {

  // Aliased because `color` is a better property name than `heroHighlight`
  @Input('heroHighlight') color: string;

  constructor(private el: ElementRef) {}

  ngOnChanges() {
    this.el.nativeElement.style.backgroundColor = this.color || 'yellow';
  }
}
```

```
<!-- app/app.component.html -->
<toh-hero-button label="OK" (change)="doSomething()">
</toh-hero-button>

<!-- `heroHighlight` is both the directive name and the data-bound aliased property name -->
<h3 heroHighlight="skyblue">The Great Bombasto</h3>
```

# Member sequence

**Do** place properties up top followed by methods.

**Do** place private members after public members, alphabetized.

**Why?** Placing members in a consistent sequence makes it easy to read and helps instantly identify which members of the component serve which purpose.

```
//app/shared/toast/toast.component.ts
/* avoid */

export class ToastComponent implements OnInit {

  private defaults = {
    title: '',
    message: 'May the Force be with you'
  };
  message: string;
  title: string;
  private toastElement: any;

  ngOnInit() {
    this.toastElement = document.getElementById('toh-toast');
  }

  // private methods
  private hide() {
    this.toastElement.style.opacity = 0;
    window.setTimeout(() => this.toastElement.style.zIndex = 0, 400);
  }

  activate(message = this.defaults.message, title = this.defaults.title) {
    this.title = title;
    this.message = message;
    this.show();
  }

  private show() {
    console.log(this.message);
    this.toastElement.style.opacity = 1;
    this.toastElement.style.zIndex = 9999;

    window.setTimeout(() => this.hide(), 2500);
  }
}
```

```
//app/shared/toast/toast.component.ts
export class ToastComponent implements OnInit {
  // public properties
  message: string;
  title: string;

  // private fields
  private defaults = {
    title: '',
    message: 'May the Force be with you'
  };
  private toastElement: any;

  // public methods
  activate(message = this.defaults.message, title = this.defaults.title) {
    this.title = title;
    this.message = message;
    this.show();
  }

  ngOnInit() {
    this.toastElement = document.getElementById('toh-toast');
  }

  // private methods
  private hide() {
    this.toastElement.style.opacity = 0;
    window.setTimeout(() => this.toastElement.style.zIndex = 0, 400);
  }

  private show() {
    console.log(this.message);
    this.toastElement.style.opacity = 1;
    this.toastElement.style.zIndex = 9999;
    window.setTimeout(() => this.hide(), 2500);
  }
}
```

# Delegate complex component logic to services

**Do** limit logic in a component to only that required for the view. All other logic should be delegated to services.

**Do** move reusable logic to services and keep components simple and focused on their intended purpose.

**Why?** Logic may be reused by multiple components when placed within a service and exposed via a function.

**Why?** Logic in a service can more easily be isolated in a unit test, while the calling logic in the component can be easily mocked.

**Why?** Removes dependencies and hides implementation details from the component.

**Why?** Keeps the component slim, trim, and focused.

```
//app/heroes/hero-list/hero-list.component.ts
/* avoid */

import { OnInit } from '@angular/core';
import { Http, Response } from '@angular/http';

import { Observable } from 'rxjs';
import { catchError, finalize, map } from 'rxjs/operators';

import { Hero } from '../shared/hero.model';

const heroesUrl = 'http://angular.io';

export class HeroListComponent implements OnInit {
  heroes: Hero[];
  constructor(private http: Http) {}
  getHeroes() {
    this.heroes = [];
    this.http.get(heroesUrl).pipe(
      map((response: Response) => <Hero[]>response.json().data),
      catchError(this.catchBadResponse),
      finalize(() => this.hideSpinner())
    ).subscribe((heroes: Hero[]) => this.heroes = heroes);
  }
  ngOnInit() {
    this.getHeroes();
  }

  private catchBadResponse(err: any, source: Observable<any>) {
    // log and handle the exception
    return new Observable();
  }

  private hideSpinner() {
    // hide the spinner
  }
}
```
```
//app/heroes/hero-list/hero-list.component.ts
import { Component, OnInit } from '@angular/core';

import { Hero, HeroService } from '../shared';

@Component({
  selector: 'toh-hero-list',
  template: `...`
})
export class HeroListComponent implements OnInit {
  heroes: Hero[];
  constructor(private heroService: HeroService) {}
  getHeroes() {
    this.heroes = [];
    this.heroService.getHeroes()
      .subscribe(heroes => this.heroes = heroes);
  }
  ngOnInit() {
    this.getHeroes();
  }
}
```

# Don't prefix _output_ properties

**Do** name events without the prefix `on`.

**Do** name event handler methods with the prefix `on` followed by the event name.

**Why?** This is consistent with built-in events such as button clicks.

**Why?** Angular allows for an [alternative syntax](https://angular.io/guide/template-syntax#binding-syntax) `on-*`. If the event itself was prefixed with `on` this would result in an `on-onEvent` binding expression.

```
//app/heroes/hero.component.ts
/* avoid */

@Component({
  selector: 'toh-hero',
  template: `...`
})
export class HeroComponent {
  @Output() onSavedTheDay = new EventEmitter<boolean>();
}
```

```
<!-- app/app.component.html -->
<!-- avoid -->

<toh-hero (onSavedTheDay)="onSavedTheDay($event)"></toh-hero>
```

---

```
//app/heroes/hero.component.ts
export class HeroComponent {
  @Output() savedTheDay = new EventEmitter<boolean>();
}
```

```
<!-- app/app.component.html -->
<toh-hero (savedTheDay)="onSavedTheDay($event)"></toh-hero>
```

# Put presentation logic in the component class

**Do** put presentation logic in the component class, and not in the template.

**Why?** Logic will be contained in one place (the component class) instead of being spread in two places.

**Why?** Keeping the component's presentation logic in the class instead of the template improves testability, maintainability, and reusability.

```
//app/heroes/hero-list/hero-list.component.ts
/* avoid */

@Component({
  selector: 'toh-hero-list',
  template: `
    <section>
      Our list of heroes:
      <hero-profile *ngFor="let hero of heroes" [hero]="hero">
      </hero-profile>
      Total powers: {{totalPowers}}<br>
      Average power: {{totalPowers / heroes.length}}
    </section>
  `
})
export class HeroListComponent {
  heroes: Hero[];
  totalPowers: number;
}
```

```
//app/heroes/hero-list/hero-list.component.ts
@Component({
  selector: 'toh-hero-list',
  template: `
    <section>
      Our list of heroes:
      <toh-hero *ngFor="let hero of heroes" [hero]="hero">
      </toh-hero>
      Total powers: {{totalPowers}}<br>
      Average power: {{avgPower}}
    </section>
  `
})
export class HeroListComponent {
  heroes: Hero[];
  totalPowers: number;

  get avgPower() {
    return this.totalPowers / this.heroes.length;
  }
}
```