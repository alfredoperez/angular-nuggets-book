# Passing Data between Routes in Angular v7.2

{% embed url="https://netbasal.com/set-state-object-when-navigating-in-angular-7-2-b87c5b977bb" %}

## Setting the state

Imperative

```typescript
@Component({
  template: `<a (click)="navigateWithState()">Go</a>`,
})
export class AppComponent  {
  constructor(public router: Router) {}
  navigateWithState() {
    this.router.navigateByUrl('/123', { state: { hello: 'world' } });
  }
}
```

Declarative

```typescript
@Component({
  selector: 'my-app',
  template: `
  <a routerLink="/details" [state]="{ hello: 'world' }">Go</a>`,
})
export class AppComponent  {}
```

## Reading the State

 Read it from the `window.history.state`

```typescript
@Component({
  selector: 'app-details-page',
  template: '<pre>{{ state$ | async | json }}</pre>'
})
export class DetailsPageComponent implements OnInit {
  state$: Observable<object>;
  
  constructor(public activatedRoute: ActivatedRoute) {}
  
  ngOnInit() {
    this.state$ = this.activatedRoute.paramMap
      .pipe(map(() => window.history.state))
  }
}
```

 Read it from the `NavigationExtras` 

```typescript
@Component({
  selector: 'app-root',
  template: `<pre>{{ state$ | async | json }}</pre>`,
})
export class AppComponent implements OnInit {
  private state$: Observable<object>;
  
  constructor(public router: Router) { }
  
  ngOnInit() {
    this.state$ =  this.router.events.pipe(
      filter(e => e instanceof NavigationStart),
      map(() => this.router.getCurrentNavigation().extras.state)
    )
  }
}
```

