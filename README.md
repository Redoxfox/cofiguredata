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

##Prestamo component
import { Component, OnInit, Output } from '@angular/core';
import { FormControl } from '@angular/forms';
import { Router } from '@angular/router';
//import * as EventEmitter from 'events';
import { entityActivoI } from 'src/app/Modelos/Activos.interface';
import { ApiService } from 'src/app/Servicios/Api/api.service';

@Component({
  selector: 'app-dashboard-activos',
  templateUrl: './dashboard-activos.component.html',
  styleUrls: ['./dashboard-activos.component.css']
})
export class DashboardActivosComponent implements OnInit {
  itemActivos:entityActivoI[] = [];
  status:string = '';
  errorMessage:string = '';

  constructor(private usuarioService:ApiService, private router:Router) {

  }

  ngOnInit(): void {
    this.usuarioService.getActivos('/api/Activos')
    .subscribe(data => {
      this.itemActivos = data;
    });
    //this.search.valueChanges.subscribe(value => this.searchEmitter)
  }

  search = new FormControl('')

 //@Output('search') searchEmitter = new EventEmitter<string>();

  EditarFila(id:number){
    this.router.navigate(['editar_activos', id]);
  }

  nuevoElemento(){
    this.router.navigate(['nuevo_activos']);
  }

  deleteActivosId(id:number){
    const url = `/api/Activos/${id}`;
    this.usuarioService.deleteActivos(url)
    .subscribe({
          next: data => {
            this.status = 'Delete successful';
            this.ngOnInit();
          },
          error: error => {
            this.errorMessage = error.message;
            console.error('There was an error!', error);
         }
    });
  }

}

 ## Servicios

import { Injectable } from '@angular/core';
import { HttpClient, HttpClientModule } from '@angular/common/http';
import { entityCategoriaTipoI, entityTipoActivoGetI, entityTipoActivoGetIdI, entityTipoActivoPostI, entityTipoActivoPutI } from 'src/app/Modelos/TipoActivos.interface';
import { entityActivoGetIdI, entityActivoI, entityActivoPostI, entityActivoPutI } from 'src/app/Modelos/Activos.interface';
import { entityConsumibleGetI, entityConsumibleGetIdI, entityConsumiblePostI, entityConsumiblePutI } from 'src/app/Modelos/Consumibles.interface';
import { entityPerifericoGetI, entityPerifericoGetIdI, entityPerifericoPostI, entityPerifericoPutI } from 'src/app/Modelos/Perifericos.interface';
import { entityActivoAsigGetI, entityUsuarioGetI, entityUsuarioGetIdI, entityUsuarioPostI, entityUsuarioPutI, entityActivoAsigPdfGetI } from 'src/app/Modelos/Usuarios.interface';

import {entityFormatoI } from 'src/app/Modelos/DataFormato.interface';
import { map } from 'rxjs/operators';
import { of } from 'rxjs';
import { OptionTipoActivoI } from 'src/app/Modelos/ObjVarios.interface';


@Injectable({
  providedIn: 'root'
})
export class ApiService {

  constructor(private HttpClient: HttpClient) {

  }

  //Metodos api tipo activos
  /*cargarUsuarios (url:string ) {

    return this.HttpClient.get<tipoActivoI[]>(url);
  }*/

  getTipoActivos(url:string){
    return this.HttpClient.get<entityTipoActivoGetI[]>(url);
  }

  getTipoActivosId(url:string){
    return this.HttpClient.get<entityTipoActivoGetIdI>(url);
  }

  postTipoActivos(url:string, entiyTipoActivo:entityTipoActivoPostI){
    return this.HttpClient.post(url,entiyTipoActivo);
  }

  putTipoActivos(url:string, entiyTipoActivo:entityTipoActivoPutI){
    return this.HttpClient.put(url,entiyTipoActivo);
  }

  deleteTipoActivos(url:string){
    return this.HttpClient.delete(url);
  }

  getCategoriaTipo(url:string){
    return this.HttpClient.get<entityCategoriaTipoI[]>(url);
  }

  getByTipoActivo(url:string){
    return this.HttpClient.get<OptionTipoActivoI[]>(url);
  }


  //Metodos api activos

 getActivos(url:string){
    return this.HttpClient.get<entityActivoI[]>(url);
  }

  getActivosId(url:string){
    return this.HttpClient.get<entityActivoGetIdI>(url);
  }

  postActivos(url:string, entiyActivo:entityActivoPostI){
    return this.HttpClient.post(url,entiyActivo);
  }

  getByActivo(url:string){
    return this.HttpClient.get<entityActivoI[]>(url);
  }

  putActivos(url:string, entiyTipoActivo:entityActivoPutI){
    return this.HttpClient.put(url,entiyTipoActivo);
  }

  deleteActivos(url:string){
    return this.HttpClient.delete(url);
  }


  //Metodos api consumibles

  getConsumibles(url:string){
    return this.HttpClient.get<entityConsumibleGetI[]>(url);
  }

  getConsumiblesId(url:string){
    return this.HttpClient.get<entityConsumibleGetIdI>(url);
  }

  getByTipoConsumibles(url:string){
    return this.HttpClient.get<entityConsumibleGetI[]>(url);
  }

  postConsumibles(url:string, entiyActivo:entityConsumiblePostI){
    return this.HttpClient.post(url,entiyActivo);
  }

  putConsumibles(url:string, entiyTipoActivo: entityConsumiblePutI){
    return this.HttpClient.put(url,entiyTipoActivo);
  }

  deleteConsumibles(url:string){
    return this.HttpClient.delete(url);
  }


  //Metodos api perifericos

  getPerifericos(url:string){
    return this.HttpClient.get<entityPerifericoGetI[]>(url);
  }

  getPerifericosId(url:string){
    return this.HttpClient.get<entityPerifericoGetIdI>(url);
  }

  getByTipoPerifericos(url:string){
    return this.HttpClient.get<entityPerifericoGetI[]>(url);
  }

  postPerifericos(url:string, entiyActivo:entityPerifericoPostI){
    return this.HttpClient.post(url,entiyActivo);
  }

  putPerifericos(url:string, entiyTipoActivo: entityPerifericoPutI){
    return this.HttpClient.put(url,entiyTipoActivo);
  }

  deletePerifericos(url:string){
    return this.HttpClient.delete(url);
  }

  //Metodos api usuarios
  getUsuarios(url:string){
    return this.HttpClient.get<entityUsuarioGetI[]>(url);
  }

  getUsuariosId(url:string){
    return this.HttpClient.get<entityUsuarioGetIdI>(url);
  }

  postUsuarios(url:string, entiyActivo:entityUsuarioPostI){
    return this.HttpClient.post(url,entiyActivo);
  }

  putUsuarios(url:string, entiyTipoActivo: entityUsuarioPutI){
    return this.HttpClient.put(url,entiyTipoActivo);
  }

  deleteUsuarios(url:string){
    return this.HttpClient.delete(url);
  }

  getByActivoAsig(url:string){
    return this.HttpClient.get<entityActivoAsigGetI[]>(url);
  }

  getRemoveActivoAsig(url:string){
    return this.HttpClient.get<entityActivoAsigGetI[]>(url);
  }

  getOnInitActivoAsig(url:string){
    return this.HttpClient.get<entityActivoAsigGetI[]>(url);
  }

  getOnInitPerifericoAsig(url:string){
    return this.HttpClient.get<entityActivoAsigGetI[]>(url);
  }

  getOnInitConsumibleAsig(url:string){
    return this.HttpClient.get<entityActivoAsigGetI[]>(url);
  }

  getDataActivosAsig(url:string){
    return this.HttpClient.get<entityFormatoI[]>(url);
  }

  getAsigForPDF(url:string){
    return this.HttpClient.get<entityActivoAsigPdfGetI[]>(url);
  }
}
  
  
##Model interface

export interface entityActivoI{
  id: number,
  nombre: string,
  modelo: string,
  serial: string,
  nroActivo: number,
  procesador: string,
  disco: string,
  color: string,
  nombreEquipo:string,
  asignado: string,
  estado: string,
  idTipo: number,
  idTipoNavigation: number,
  usuarioActivos: []
}
  
##component

import { Component, OnInit, Output } from '@angular/core';
import { FormControl } from '@angular/forms';
import { Router } from '@angular/router';
//import * as EventEmitter from 'events';
import { entityActivoI } from 'src/app/Modelos/Activos.interface';
import { ApiService } from 'src/app/Servicios/Api/api.service';

@Component({
  selector: 'app-dashboard-activos',
  templateUrl: './dashboard-activos.component.html',
  styleUrls: ['./dashboard-activos.component.css']
})
export class DashboardActivosComponent implements OnInit {
  itemActivos:entityActivoI[] = [];
  status:string = '';
  errorMessage:string = '';

  constructor(private usuarioService:ApiService, private router:Router) {

  }

  ngOnInit(): void {
    this.usuarioService.getActivos('/api/Activos')
    .subscribe(data => {
      this.itemActivos = data;
    });
    //this.search.valueChanges.subscribe(value => this.searchEmitter)
  }

  search = new FormControl('')

 //@Output('search') searchEmitter = new EventEmitter<string>();

  EditarFila(id:number){
    this.router.navigate(['editar_activos', id]);
  }

  nuevoElemento(){
    this.router.navigate(['nuevo_activos']);
  }

  deleteActivosId(id:number){
    const url = `/api/Activos/${id}`;
    this.usuarioService.deleteActivos(url)
    .subscribe({
          next: data => {
            this.status = 'Delete successful';
            this.ngOnInit();
          },
          error: error => {
            this.errorMessage = error.message;
            console.error('There was an error!', error);
         }
    });
  }

}
  
 ##html component
  <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Activos TI</title>


</head>
    <app-header></app-header>
    <body>
    <div class="col mt-4 p-3 border">
      <div class="row ">
        <div class="col">
          <button type="button" class="btn btn-primary"  (click)="nuevoElemento()">Nuevo Registro</button>
        </div>
        <div class="col">
          <input type="text" class="form-control"  placeholder="Nombre">
        </div>
        <div class="col">
          <i class="fas fa-search" style="margin-right: 15px;" ></i>
        </div>
      </div>
    </div>

    <div class="container mt-4" >
      <div class="card">
          <div class="card-body">
            <span class="h3">Lista Activos</span>
            <table class="table">
              <thead>
                <tr>
                  <th scope="col">#</th>
                  <th scope="col">Nombre</th>
                  <th scope="col">Modelo</th>
                  <th scope="col">Serial</th>
                  <th scope="col">Nro Activo</th>
                  <th scope="col">Color</th>
                  <th scope="col">Nombre Equipo</th>
                  <th scope="col">Asinado</th>
                  <th scope="col">Estado</th>
                  <th scope="col">Id Tipo</th>
                  <th scope="col">Editar</th>
                  <th scope="col">Eliminar</th>
                </tr>
              </thead>
              <tbody>
                <tr *ngFor="let item of itemActivos; let indice=index" >
                  <td>{{indice + 1}}</td>
                  <td>{{item.nombre}}</td>
                  <td>{{item.modelo}}</td>
                  <td>{{item.serial}}</td>
                  <td>{{item.nroActivo}}</td>
                  <td>{{item.color}}</td>
                  <td>{{item.nombreEquipo}}</td>
                  <td>{{item.asignado}}</td>
                  <td>{{item.estado}}</td>
                  <td scope="row">{{item.idTipo}}</td>
                  <td>
                    <i class="fas fa-edit text-info " style="margin-right: 7px;" (click)="EditarFila(item.id)"></i>
                  </td>
                  <td>
                    <i class="fas fa-trash-alt text-danger " (click)="deleteActivosId(item.id)"></i>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
      </div>
    </div>
</body>
</html>









