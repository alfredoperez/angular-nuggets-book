# Improving ngFor using trackBy pipe



{% embed url="https://www.bennadel.com/blog/3579-using-pure-pipes-to-generate-ngfor-trackby-identity-functions-in-angular-7-2-7.htm?utm\_campaign=NG-Newsletter&utm\_medium=email&utm\_source=NG-Newsletter\_296" %}

Code

{% code-tabs %}
{% code-tabs-item title="track-by-property.pipe.ts" %}
```typescript

// Import the core angular services.
import { Pipe } from "@angular/core";
import { PipeTransform } from "@angular/core";
 
// ----------------------------------------------------------------------------------- //
// ----------------------------------------------------------------------------------- //
 
interface TrackByFunctionCache {
    [ propertyName: string ]: <T>( index: number, item: T ) => any;
}
 
// Since the resultant TrackBy functions are based purely on a static property name, we
// can cache these Functions across the entire app. No need to generate more than one
// Function for the same property.
var cache: TrackByFunctionCache = Object.create( null );
 
@Pipe({
    name: "trackByProperty",
    pure: true
})
export class TrackByPropertyPipe implements PipeTransform {
 
    // I return a TrackBy function that plucks the given property from the ngFor item.
    public transform( propertyName: string ) : Function {
 
        console.warn( `Getting track-by for [${ propertyName }].` );
 
        // Ensure cached function exists.
        if ( ! cache[ propertyName ] ) {
 
            cache[ propertyName ] = function trackByProperty<T>( index: number, item: T ) : any {
 
                return( item[ propertyName ] );
 
            };
 
        }
 
        return( cache[ propertyName ] );
 
    }
 
}
```
{% endcode-tabs-item %}

{% code-tabs-item title="demo.component.ts" %}
```typescript
// Import the core angular services.
import { Component } from "@angular/core";
 
// ----------------------------------------------------------------------------------- //
// ----------------------------------------------------------------------------------- //
 
interface Friend {
    id: number;
    name: string;
}
 
@Component({
    selector: "my-app",
    styleUrls: [ "./app.component.less" ],
    template:
    `
        <h2>
            Friends
        </h2>
        <p>
            <a (click)="cycleFriends()">Cycle friends</a>
            &mdash;
            <a (click)="toggleFriends()">Toggle friends</a>
        </p>
        <ul *ngIf="isShowingFriends">
            <ng-template
                ngFor
                let-friend
                [ngForOf]="friends"
                [ngForTrackBy]="( 'id' | trackByProperty )">
 
                <li [mySpy]="friend.name">
                    {{ friend.name }}
                </li>
 
            </ng-template>
        </ul>
    `
})
export class AppComponent {
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}





