[[_TOC_]]

Note: The following guide has been adapted from the [official Angular Style Guidelines](https://angular.io/guide/styleguide#directives)

# Use directives to enhance an element

**Do** use attribute directives when you have presentation logic without a template.

**Why?** Attribute directives don't have an associated template.

**Why?** An element may have more than one attribute directive applied.

```
//app/shared/highlight.directive.ts
@Directive({
  selector: '[tohHighlight]'
})
export class HighlightDirective {
  @HostListener('mouseover') onMouseEnter() {
    // do highlight work
  }
}
```

```
<!-- app/app.component.html -->
<div tohHighlight>Bombasta</div>
```

# _HostListener_/_HostBinding_ decorators versus _host_ metadata

**Consider** preferring the `@HostListener` and `@HostBinding` to the `host` property of the `@Directive` and `@Component` decorators.

**Do** be consistent in your choice.

**Why?** The property associated with `@HostBinding` or the method associated with `@HostListener` can be modified only in a single place&mdash;in the directive's class. If you use the `host` metadata property, you must modify both the property/method declaration in the directive's class and the metadata in the decorator associated with the directive.

```
//app/shared/validator.directive.ts
import { Directive, HostBinding, HostListener } from '@angular/core';

@Directive({
  selector: '[tohValidator]'
})
export class ValidatorDirective {
  @HostBinding('attr.role') role = 'button';
  @HostListener('mouseenter') onMouseEnter() {
    // do work
  }
}
```

Compare with the less preferred `host` metadata alternative.

**Why?** The `host` metadata is only one term to remember and doesn't require extra ES imports.

```
//app/shared/validator2.directive.ts
import { Directive } from '@angular/core';

@Directive({
  selector: '[tohValidator2]',
  host: {
    '[attr.role]': 'role',
    '(mouseenter)': 'onMouseEnter()'
  }
})
export class Validator2Directive {
  role = 'button';
  onMouseEnter() {
    // do work
  }
}
```