[[_TOC_]]

Note: The following guide has been adapted from the [official Angular Style Guidelines](https://angular.io/guide/styleguide#services)

# Services are singletons

**Do** use services as singletons within the same injector. Use them for sharing data and functionality.

**Why?** Services are ideal for sharing methods across a feature area or an app.

**Why?** Services are ideal for sharing stateful in-memory data.

```
//app/heroes/shared/hero.service.ts
export class HeroService {
  constructor(private http: Http) { }

  getHeroes() {
    return this.http.get('api/heroes').pipe(
      map((response: Response) => <Hero[]>response.json()));
  }
}
```

# Single responsibility

**Do** create services with a single responsibility that is encapsulated by its context.

**Do** create a new service once the service begins to exceed that singular purpose.

**Why?** When a service has multiple responsibilities, it becomes difficult to test.

**Why?** When a service has multiple responsibilities, every component or service that injects it now carries the weight of them all.

# Providing a service

**Do** provide a service with the app root injector in the `@Injectable` decorator of the service.

**Why?** The Angular injector is hierarchical.

**Why?** When you provide the service to a root injector, that instance of the service is shared and available in every class that needs the service. This is ideal when a service is sharing methods or state.

**Why?** When you register a service in the `@Injectable` decorator of the service, optimization tools such as those used by the [Angular CLI's](cli) production builds can perform tree shaking and remove services that aren't used by your app.

**Why?** This is not ideal when two different components need different instances of a service. In this scenario it would be better to provide the service at the component level that needs the new and separate instance.

```
//src/app/treeshaking/service.ts
@Injectable({
  providedIn: 'root',
})
export class Service {
}
```

# Use the @Injectable() class decorator

**Do** use the `@Injectable()` class decorator instead of the `@Inject` parameter decorator when using types as tokens for the dependencies of a service.

**Why?** The Angular Dependency Injection (DI) mechanism resolves a service's own dependencies based on the declared types of that service's constructor parameters.

**Why?** When a service accepts only dependencies associated with type tokens, the `@Injectable()` syntax is much less verbose compared to using `@Inject()` on each individual constructor parameter.

```
//app/heroes/shared/hero-arena.service.ts
/* avoid */

export class HeroArena {
  constructor(
      @Inject(HeroService) private heroService: HeroService,
      @Inject(Http) private http: Http) {}
}
```
```
//app/heroes/shared/hero-arena.service.ts
@Injectable()
export class HeroArena {
  constructor(
    private heroService: HeroService,
    private http: Http) {}
}
```