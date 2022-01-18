# cofiguredata

#archivo app.module.ts

import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppRoutingModule } from './app-routing.module';
import { AppRoutingComponent } from './app-routing.module';
import { ReactiveFormsModule, FormsModule } from '@angular/forms';
import {HttpClientModule} from '@angular/common/http'
import { AppComponent } from './app.component';
import { HeaderComponent } from './header/header.component';



@NgModule({
  declarations: [
    AppComponent,
    AppRoutingComponent,
    HeaderComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    ReactiveFormsModule,
    FormsModule,
    HttpClientModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }

##Archivo app-routing.ts

import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
//Lineas para importar rutas para componentes
import { HeaderComponent } from './header/header.component';


const routes: Routes = [
  //Agregar ruta por defecto login
  {path:'',redirectTo:'header', pathMatch:'full'},
  //Agregar path de rutas
  {path:'header', component:HeaderComponent},
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }

export const  AppRoutingComponent = [
  HeaderComponent,FormatoEntregaComponent
];

##Html

<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>ActivosTI</title>
  <base href="/">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="icon" type="image/x-icon" href="favicon.ico">
  <link rel="stylesheet" href="https://pro.fontawesome.com/releases/v5.10.0/css/all.css" integrity="sha384-AYmEC3Yw5cVb3ZcuHtOA93w35dYTsvhLPVnYs9eStHfGJvOvKxVfELGroGkvsg+p" crossorigin="anonymous"/>
</head>
<body>
  <app-root></app-root>
</body>
</html>

##Archivo angular.js

{
            "styles": [
              "src/styles.css",
              "node_modules/bootstrap/dist/css/bootstrap.min.css"
            ],
            "scripts": [
              "node_modules/jquery/dist/jquery.min.js",
              "node_modules/bootstrap/dist/js/bootstrap.min.js"
            ]
}

##Archivo header .ts

import { Component, OnInit } from '@angular/core';
import { Router } from '@angular/router';

@Component({
  selector: 'app-header',
  templateUrl: './header.component.html',
  styleUrls: ['./header.component.css']
})
export class HeaderComponent implements OnInit {

  constructor(private router:Router) { }

  ngOnInit(): void {
  }

  VerTipoActivo(){
    this.router.navigate(['dashboard_tipoActivo']);
  }

  VerActivos(){
    this.router.navigate(['dashboard_activos']);
  }

  VerPerifericos(){
    this.router.navigate(['dashboard_perifericos']);
  }

  VerConsumibles(){
    this.router.navigate(['dashboard_consumibles']);
  }

  VerUsuarios(){
    this.router.navigate(['dashboard_usuarios']);
  }

  Verformato(){
    this.router.navigate(['formato_entrega']);
  }

}

##Archivo header .html

<nav class="navbar navbar-expand-lg navbar-dark bg-dark">
  <a class="navbar-brand" href="#">GESTION ACTIVOS TI</a>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>

  <div class="collapse navbar-collapse" id="navbarSupportedContent">
    <ul class="navbar-nav mr-auto">
      <li class="nav-item active">
        <a class="nav-link" (click)="VerTipoActivo()">Tipo Activo</a>
      </li>
      <li class="nav-item active">
        <a class="nav-link" (click)="VerActivos()">Activos</a>
      </li>
      <li class="nav-item">
        <a class="nav-link" (click)="VerPerifericos()">Perifericos</a>
      </li>
      <li class="nav-item">
        <a class="nav-link" (click)="VerConsumibles()">Consuimibles</a>
      </li>
      <li class="nav-item">
        <a class="nav-link" (click)="VerUsuarios()">Usuarios</a>
      </li>
      <li class="nav-item">
        <a class="nav-link" (click)="Verformato()">Formato</a>
      </li>
    </ul>

  </div>
</nav>







