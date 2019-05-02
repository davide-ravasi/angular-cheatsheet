# ROUTING
## In 

<code>
import { RouterModule, Routes } from '@angular/router';

const appRoutes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'users', component: UsersComponent , children: [
        { path: ':id/:name', component: UserComponent }
   ] },
  { path: 'servers', component: ServersComponent , children: [
      { path: ':id', component: ServerComponent },
      { path: ':id/edit', component: EditServerComponent } 
  ]},
 { path: '',
    redirectTo: '/heroes',
    pathMatch: 'full'
  },
  { path: '**', component: PageNotFoundComponent }
];
</code>

## imports:

<code>
 RouterModule.forRoot(
      appRoutes,
      { enableTracing: true } // <-- debugging purposes only
    )
</code>

## to load component:

<code><router-outlet></router-outlet></code>


## in tag link html

<code>
<a [routerLink]="['/']" routerLinkActive="active" [routerLinkActiveOptions]="{exact: true}">Home</a>
<a [routerLink]="['/about']" routerLinkActive="active">About</a>

      <a
        [routerLink]="['/servers', server.id]"
        [queryParams]="{allowEdit: true}" 
        fragment="loading"
        class="list-group-item"
        *ngFor="let server of servers">
</code>

## in javascript

<code>
import { ActivatedRoute, Params } from '@angular/router';

constructor(private route: ActivatedRoute) { }

this.router.navigate(['/servers',id,'edit']);

this._router.navigate(['detail'], { queryParams: { pageNum: this.pageNum + 1 }, relativeTo: this._Activatedroute } );
</code>
[https://www.tektutorialshub.com/angular/angular-navigating-between-routes/](https://www.tektutorialshub.com/angular/angular-navigating-between-routes/)


## to retrieve in component :

<code>    
this.snapshotPageNo = this.Activatedroute.snapshot.queryParams['pageNum'] || 0;
     
    this.Activatedroute.params
        .subscribe(params => { 
            this.pageNum = params['pageNum']||0;
           console.log('Query params ',this.pageNum) 
    });


	this.Activatedroute.queryParams

	this.Activatedroute.fragment
</code>

[https://www.tektutorialshub.com/angular/angular-passing-optional-query-parameters-to-route/](https://www.tektutorialshub.com/angular/angular-passing-optional-query-parameters-to-route/)

<code>
	this.router.navigate(['/home'], { fragment: 'top' });
</code>


## to preserve the query if we click another link in javascript

<code>
	this.router.navigate(['/servers',id,'edit'], {queryParamsHandling: 'preserve'});
</code>

***

# CUSTOM DIRECTIVES

directive to higlight an element with param:

<code>
import {Directive, Renderer2, ElementRef, HostListener, Input} from '@angular/core';

@Directive({
  selector: '[appHighlight]'
})
export class HighlightDirective {
 
  @Input('appHighlight') highlightColor: string;

  private _defaultColor = 'red';

  constructor(private _el: ElementRef, private _renderer: Renderer2) {
    this._renderer.setStyle(this._el.nativeElement, 'color', this._defaultColor);
  }

  @HostListener('mouseenter') onMouseEnter() {
    this._renderer.setStyle(this._el.nativeElement, 'color', this.highlightColor);
  }

  @HostListener('mouseleave') onMouseLeave() {
    this._renderer.setStyle(this._el.nativeElement, 'color', this._defaultColor);
  }


}


</code>

## in html

<code>
<div [appHighlight]="'yellow'">Texte en highlight</div>
</code>

## with @hostBinding

<code>
import { Directive, HostBinding, HostListener } from '@angular/core';

@Directive({
  selector: '[appDropdown]'
})
export class DropdownDirective {
  @HostBinding('class.open') isOpen: boolean = false;

  constructor() { }
    
    
  @HostListener('click') clickElement(EventData: Event) {
        this.isOpen = !this.isOpen;      
    }
}
</code>

[http://www.learn-angular.fr/les-directives/](http://www.learn-angular.fr/les-directives/)






