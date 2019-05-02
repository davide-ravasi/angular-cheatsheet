# ROUTING
## In 

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

## imports:


	RouterModule.forRoot(
		appRoutes,
		{ enableTracing: true } // <-- debugging purposes only
	)


## to load component:

	<router-outlet></router-outlet>



## in tag link html


	<a [routerLink]="['/']" routerLinkActive="active" [routerLinkActiveOptions]="{exact: true}">Home</a>
	<a [routerLink]="['/about']" routerLinkActive="active">About</a>

	      <a
		[routerLink]="['/servers', server.id]"
		[queryParams]="{allowEdit: true}" 
		fragment="loading"
		class="list-group-item"
		*ngFor="let server of servers">


## in javascript


	import { ActivatedRoute, Params } from '@angular/router';

	constructor(private route: ActivatedRoute) { }

	this.router.navigate(['/servers',id,'edit']);

	this._router.navigate(['detail'], { queryParams: { pageNum: this.pageNum + 1 }, relativeTo: this._Activatedroute } 	);


[https://www.tektutorialshub.com/angular/angular-navigating-between-routes/](https://www.tektutorialshub.com/angular/angular-navigating-between-routes/)


## to retrieve in component :


	this.snapshotPageNo = this.Activatedroute.snapshot.queryParams['pageNum'] || 0;
     
	this.Activatedroute.params
	.subscribe(params => { 
	    this.pageNum = params['pageNum']||0;
	   console.log('Query params ',this.pageNum) 
	});


	this.Activatedroute.queryParams

	this.Activatedroute.fragment


[https://www.tektutorialshub.com/angular/angular-passing-optional-query-parameters-to-route/](https://www.tektutorialshub.com/angular/angular-passing-optional-query-parameters-to-route/)


	this.router.navigate(['/home'], { fragment: 'top' });



## to preserve the query if we click another link in javascript


	this.router.navigate(['/servers',id,'edit'], {queryParamsHandling: 'preserve'});


***

# CUSTOM DIRECTIVES

directive to higlight an element with param:


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




## in html


		<div [appHighlight]="'yellow'">Texte en highlight</div>


## with @hostBinding


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


[http://www.learn-angular.fr/les-directives/](http://www.learn-angular.fr/les-directives/)






