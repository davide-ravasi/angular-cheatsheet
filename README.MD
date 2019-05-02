# ROUTING
## In 

<code>import { RouterModule, Routes } from '@angular/router';

const appRoutes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'users', component: UsersComponent , children: [
        { path: ':id/:name', component: UserComponent }
   ] },
  { path: 'servers', component: ServersComponent , children: [
      { path: ':id', component: ServerComponent },
      { path: ':id/edit', component: EditServerComponent } 
  ]}  
];</code>

## imports:

<code>    RouterModule.forRoot(
      appRoutes,
      { enableTracing: true } // <-- debugging purposes only
    )
</code>
## to load component:

<code><router-outlet></router-outlet></code>


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

this._router.navigate(['detail'], { queryParams: { pageNum: this.pageNum + 1 }, relativeTo: this._Activatedroute } );

[https://www.tektutorialshub.com/angular/angular-navigating-between-routes/](https://www.tektutorialshub.com/angular/angular-navigating-between-routes/)

## to retrieve in component :

    this.snapshotPageNo = this.Activatedroute.snapshot.queryParams['pageNum'] || 0;
     
    this.Activatedroute.queryParams
        .subscribe(params => { 
            this.pageNum = +params['pageNum']||0;
           console.log('Query params ',this.pageNum) 
    });

[https://www.tektutorialshub.com/angular/angular-passing-optional-query-parameters-to-route/](https://www.tektutorialshub.com/angular/angular-passing-optional-query-parameters-to-route/)

this.router.navigate(['/home'], { fragment: 'top' });





