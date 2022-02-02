# cofiguredata

mysqlclient
https://www.c-sharpcorner.com/UploadFile/9582c9/insert-update-delete-display-data-in-mysql-using-C-Sharp/

#environment

export const environment = {
  production: false,
   //apiUrl: "http://172.25.85.31:8081/"
   apiUrl: "http://localhost:22224/",
   //apiUrl: "https://localhost:44384/",
   //apiUrlIOTec: "http://172.25.80.55:8011/"
};

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
  
  ##cors
  
  {
  "/api/TipoActivo":{
      "target":"https://localhost:44389",
      "secure":false,
      "logLevel":"debug",
      "changeOrigin":true
  },

  "/api/TipoActivo/CategoriaTipo":{
    "target":"https://localhost:44389",
    "secure":false,
    "logLevel":"debug",
    "changeOrigin":true
  },

  "/api/TipoActivo/*":{
    "target":"https://localhost:44389",
    "secure":false,
    "logLevel":"debug",
    "changeOrigin":true
  },

  "/api/Activos/":{
    "target":"https://localhost:44389",
    "secure":false,
    "logLevel":"debug",
    "changeOrigin":true
  },

  "/api/Activos/*":{
    "target":"https://localhost:44389",
    "secure":false,
    "logLevel":"debug",
    "changeOrigin":true
  },

  "/api/Consumibles":{
    "target":"https://localhost:44389",
    "secure":false,
    "logLevel":"debug",
    "changeOrigin":true
  },

  "/api/Consumibles/*":{
    "target":"https://localhost:44389",
    "secure":false,
    "logLevel":"debug",
    "changeOrigin":true
  },

  "/api/Perifericos":{
    "target":"https://localhost:44389",
    "secure":false,
    "logLevel":"debug",
    "changeOrigin":true
  },

  "/api/Perifericos/*":{
    "target":"https://localhost:44389",
    "secure":false,
    "logLevel":"debug",
    "changeOrigin":true
  },

  "/api/Usuarios/*":{
    "target":"https://localhost:44389",
    "secure":false,
    "logLevel":"debug",
    "changeOrigin":true
  },

  "/api/Usuarios":{
    "target":"https://localhost:44389",
    "secure":false,
    "logLevel":"debug",
    "changeOrigin":true
  }

}
  
#Component edit
  
import { Component, OnInit } from '@angular/core';
import { FormBuilder, FormGroup, Validators } from '@angular/forms';
import { ActivatedRoute, Router } from '@angular/router';
import { entityActivoPutI } from 'src/app/Modelos/Activos.interface';
import { ApiService } from 'src/app/Servicios/Api/api.service';
import { environment } from 'src/environments/environment';

@Component({
  selector: 'app-editar-activos',
  templateUrl: './editar-activos.component.html',
  styleUrls: ['./editar-activos.component.css']
})
export class EditarActivosComponent implements OnInit {
  updateActivo: FormGroup;
  submitted = false;
  itemActivos=<entityActivoPutI>{};
  id:number = 0 ;
  idTipo:number = 0;
  ActivosController:string= '';
  constructor(private formB:FormBuilder,
    private usuarioService:ApiService,
    private router:Router,
    private arouter:ActivatedRoute,
    public dataService:ApiService) {
    this.updateActivo = this.formB.group({
      id:['',Validators.required],
      nombre:['',Validators.required],
      modelo: ['',Validators.required],
      serial: ['',Validators.required],
      nroActivo: ['',Validators.required],
      procesador:['',Validators.required],
      disco: ['',Validators.required],
      color: ['',Validators.required],
      nombreEquipo:['',Validators.required],
      asignado: ['',Validators.required],
      estado: ['',Validators.required]
    })
  }

  ngOnInit(): void {
    this.id=Number(this.arouter.snapshot.params.id);
    this.ActivosController = "api/Activos";
    const url = `${environment.apiUrl}${this.ActivosController}` + `/${this.id}`;
    this.usuarioService.getActivosId(url)
    .subscribe(data => {
      this.updateActivo.controls["nombre"].setValue(data.nombre);
      this.updateActivo.controls["modelo"].setValue(data.modelo);
      this.updateActivo.controls["serial"].setValue(data.serial);
      this.updateActivo.controls["nroActivo"].setValue(data.nroActivo);
      this.updateActivo.controls["procesador"].setValue(data.procesador);
      this.updateActivo.controls["disco"].setValue(data.disco);
      this.updateActivo.controls["color"].setValue(data.color);
      this.updateActivo.controls["nombreEquipo"].setValue(data.nombreEquipo);
      this.updateActivo.controls["asignado"].setValue(data.asignado);
      this.updateActivo.controls["estado"].setValue(data.estado);
      this.idTipo = data.idTipo;
    });
  }

  updataActivo(){

    this.itemActivos= {
      id:this.id,
      nombre: this.updateActivo.value.nombre,
      modelo: this.updateActivo.value.modelo,
      serial: this.updateActivo.value.serial,
      nroActivo: this.updateActivo.value.nroActivo,
      procesador: this.updateActivo.value.procesador,
      disco: this.updateActivo.value.disco,
      color: this.updateActivo.value.color,
      nombreEquipo: this.updateActivo.value.nombreEquipo,
      asignado:this.updateActivo.value.asignado,
      estado:this.updateActivo.value.estado,
      idTipo:this.idTipo
    }
    ;
    const url = `${environment.apiUrl}${this.ActivosController}` +`/${this.id}`;
    this.usuarioService.putActivos(url, this.itemActivos)
    .subscribe(data => {
      console.log(data);
      this.router.navigate(['dashboard_activos']);
    });

  }

}

#component new
  
import { Component, OnInit } from '@angular/core';
import { FormBuilder, FormGroup, Validators } from '@angular/forms';
import { ActivatedRoute, Router } from '@angular/router';
import { entityActivoI, entityActivoPostI } from 'src/app/Modelos/Activos.interface';
import { entityTipoActivoGetI } from 'src/app/Modelos/TipoActivos.interface';
import { ApiService } from 'src/app/Servicios/Api/api.service';
import { environment } from 'src/environments/environment';

@Component({
  selector: 'app-nuevo-activos',
  templateUrl: './nuevo-activos.component.html',
  styleUrls: ['./nuevo-activos.component.css']
})
export class NuevoActivosComponent implements OnInit {
  createNewActivo: FormGroup;
  itemActivos=<entityActivoPostI>{};
  itemTipoActivosAll:entityTipoActivoGetI[] = [];
  itemTipoActivos:entityActivoI[] = [];
  TipoActivoController:string= '';
  ActivosController:string= '';
  constructor(private formB:FormBuilder,
    private usuarioService:ApiService,
    private router:Router,
    private arouter:ActivatedRoute) {
      this.createNewActivo = this.formB.group({
        nombre:['',Validators.required],
        modelo: ['',Validators.required],
        serial: ['',Validators.required],
        nroActivo: ['',Validators.required],
        procesador:['',Validators.required],
        disco: ['',Validators.required],
        color: ['',Validators.required],
        nombreEquipo:['',Validators.required],
        asignado: ['',Validators.required],
        estado: ['',Validators.required],
        idTipo: ['',Validators.required]
      })
     }

  ngOnInit(): void {
    this.TipoActivoController = "api/TipoActivo/";
    this.usuarioService.getTipoActivos(`${environment.apiUrl}${this.TipoActivoController}`)
    .subscribe(data => {
      this.itemTipoActivosAll = data;
    });
  }

  agregarActivo(){

    this.itemActivos= {
      nombre:this.createNewActivo.value.nombre,
      modelo: this.createNewActivo.value.modelo,
      serial: this.createNewActivo.value.serial,
      nroActivo:this.createNewActivo.value.nroActivo,
      procesador: this.createNewActivo.value.procesador,
      disco: this.createNewActivo.value.disco,
      color: this.createNewActivo.value.color,
      nombreEquipo:this.createNewActivo.value.nombreEquipo,
      asignado: "DISPONIBLE",
      estado: "BUENO",
      idTipo: this.createNewActivo.value.idTipo
    }
    this.ActivosController = "api/Activos";
    const url = `${environment.apiUrl}${this.ActivosController}`;
    this.usuarioService.postActivos(url, this.itemActivos)
    .subscribe(data => {
      console.log(this.itemActivos);
      this.router.navigate(['dashboard_activos']);
    });

  }


}

 #Html Edit component
 
 <app-header></app-header>
<div class="container pt-4">
  <div class="row">
      <div class="col-lg-6 offset-lg-3">
          <div class="card">
              <div class="card-body">
                <span class="h3">Nuevo Tipo Activo</span>
                  <form class="mt-4" [formGroup]="updateActivo" (ngSubmit)="updataActivo()">
                    <div class="row">
                      <div class="col">
                          <input type="text" class="form-control" formControlName="nombre" placeholder="Nombre">
                      </div>
                      <div class="col">
                          <input type="text" class="form-control" formControlName="modelo" placeholder="Modelo">
                      </div>
                    </div>
                    <div class="row mt-2">
                        <div class="col">
                            <input type="text" class="form-control" formControlName="serial" placeholder="Serial">
                        </div>
                        <div class="col">
                            <input type="text" class="form-control" formControlName="nroActivo" placeholder="Numero Activo">
                        </div>
                    </div>
                    <div class="row mt-2">
                        <div class="col">
                            <input type="text" class="form-control" formControlName="procesador" placeholder="Procesador">
                        </div>
                        <div class="col ">
                            <input type="text" class="form-control" formControlName="disco" placeholder="Disco">
                        </div>
                    </div>
                    <div class="row mt-2">
                        <div class="col">
                            <input type="text" class="form-control" formControlName="color" placeholder="Color">
                        </div>
                        <div class="col">
                            <input type="text" class="form-control" formControlName="nombreEquipo" placeholder="Nombre de Red">
                        </div>
                    </div>

                    <div class="row mt-2">
                      <div class="col">
                          <input type="text" class="form-control" formControlName="asignado" placeholder="ASIGNADO">
                      </div>
                    </div>
                    <div class="mt-3">
                        <button type="text" class="btn btn-primary" style="margin-right: 7px;">Volver</button>
                        <button type="submit" class="btn btn-primary">Actulizar</button>
                    </div>
                  </form>
              </div>
          </div>
      </div>
  </div>
</div>

#Html component new

<app-header></app-header>
<div class="container pt-4">
  <div class="row">
      <div class="col-lg-6 offset-lg-3">
          <div class="card">
              <div class="card-body">
                  <h5>Agregra Nuevo Activo</h5>
                  <form class="mt-4" [formGroup]="createNewActivo" (ngSubmit)="agregarActivo()">
                      <div class="row">
                          <div class="col">
                              <input type="text" class="form-control" formControlName="nombre" placeholder="Nombre">
                          </div>
                          <div class="col">
                              <input type="text" class="form-control" formControlName="modelo" placeholder="Modelo">
                          </div>
                      </div>
                      <div class="row mt-2">
                          <div class="col">
                              <input type="text" class="form-control" formControlName="serial" placeholder="Serial">
                          </div>
                          <div class="col">
                              <input type="text" class="form-control" formControlName="nroActivo" placeholder="Numero Activo">
                          </div>
                      </div>
                      <div class="row mt-2">
                          <div class="col">
                              <input type="text" class="form-control" formControlName="procesador" placeholder="Procesador">
                          </div>
                          <div class="col ">
                              <input type="text" class="form-control" formControlName="disco" placeholder="Disco">
                          </div>
                      </div>
                      <div class="row mt-2">
                          <div class="col">
                              <input type="text" class="form-control" formControlName="color" placeholder="Color">
                          </div>
                          <div class="col">
                              <input type="text" class="form-control" formControlName="nombreEquipo" placeholder="Nombre de Red">
                          </div>
                      </div>
                      <div class="row m-3">
                         <select formControlName="idTipo" >
                              <option *ngFor = "let item of itemTipoActivosAll" value={{item.id}}>
                                 {{item.nombre}}
                              </option>
                         </select>
                      </div>
                      <div class="mt-3">
                          <button type="text" class="btn btn-primary" style="margin-right: 7px;">Volver</button>
                          <button type="submit" class="btn btn-primary">Agregar</button>
                      </div>
                  </form>
              </div>
          </div>
      </div>
  </div>
</div>

#component new
import { Component, OnInit } from '@angular/core';
import { FormBuilder, FormGroup, Validators } from '@angular/forms';
import { ActivatedRoute, Router } from '@angular/router';
import { entityActivoI, entityActivoPostI } from 'src/app/Modelos/Activos.interface';
import { entityTipoActivoGetI } from 'src/app/Modelos/TipoActivos.interface';
import { ApiService } from 'src/app/Servicios/Api/api.service';
import { environment } from 'src/environments/environment';

@Component({
  selector: 'app-nuevo-activos',
  templateUrl: './nuevo-activos.component.html',
  styleUrls: ['./nuevo-activos.component.css']
})
export class NuevoActivosComponent implements OnInit {
  createNewActivo: FormGroup;
  itemActivos=<entityActivoPostI>{};
  itemTipoActivosAll:entityTipoActivoGetI[] = [];
  itemTipoActivos:entityActivoI[] = [];
  TipoActivoController:string= '';
  ActivosController:string= '';
  constructor(private formB:FormBuilder,
    private usuarioService:ApiService,
    private router:Router,
    private arouter:ActivatedRoute) {
      this.createNewActivo = this.formB.group({
        nombre:['',Validators.required],
        modelo: ['',Validators.required],
        serial: ['',Validators.required],
        nroActivo: ['',Validators.required],
        procesador:['',Validators.required],
        disco: ['',Validators.required],
        color: ['',Validators.required],
        nombreEquipo:['',Validators.required],
        asignado: ['',Validators.required],
        estado: ['',Validators.required],
        idTipo: ['',Validators.required]
      })
     }

  ngOnInit(): void {
    this.TipoActivoController = "api/TipoActivo/";
    this.usuarioService.getTipoActivos(`${environment.apiUrl}${this.TipoActivoController}`)
    .subscribe(data => {
      this.itemTipoActivosAll = data;
    });
  }

  agregarActivo(){

    this.itemActivos= {
      nombre:this.createNewActivo.value.nombre,
      modelo: this.createNewActivo.value.modelo,
      serial: this.createNewActivo.value.serial,
      nroActivo:this.createNewActivo.value.nroActivo,
      procesador: this.createNewActivo.value.procesador,
      disco: this.createNewActivo.value.disco,
      color: this.createNewActivo.value.color,
      nombreEquipo:this.createNewActivo.value.nombreEquipo,
      asignado: "DISPONIBLE",
      estado: "BUENO",
      idTipo: this.createNewActivo.value.idTipo
    }
    this.ActivosController = "api/Activos";
    const url = `${environment.apiUrl}${this.ActivosController}`;
    this.usuarioService.postActivos(url, this.itemActivos)
    .subscribe(data => {
      console.log(this.itemActivos);
      this.router.navigate(['dashboard_activos']);
    });

  }


}









