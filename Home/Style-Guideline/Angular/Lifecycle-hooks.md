[[_TOC_]]

Note: The following guide has been adapted from the [official Angular Style Guidelines](https://angular.io/guide/styleguide#lifecycle-hooks)

Use Lifecycle hooks to tap into important events exposed by Angular.

# Implement lifecycle hook interfaces

**Do** implement the lifecycle hook interfaces.

**Why?** Lifecycle interfaces prescribe typed method signatures. use those signatures to flag spelling and syntax mistakes.

```
//app/heroes/shared/hero-button/hero-button.component.ts
/* avoid */

@Component({
  selector: 'toh-hero-button',
  template: `<button>OK<button>`
})
export class HeroButtonComponent {
  onInit() { // misspelled
    console.log('The component is initialized');
  }
}
```
```
//app/heroes/shared/hero-button/hero-button.component.ts
@Component({
  selector: 'toh-hero-button',
  template: `<button>OK</button>`
})
export class HeroButtonComponent implements OnInit {
  ngOnInit() {
    console.log('The component is initialized');
  }
}
```