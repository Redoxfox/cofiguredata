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
import { FooterComponent } from './footer/footer.component';
import { AsignacionActivosComponent } from './Usuarios/asignacion-activos/asignacion-activos.component';
import { FormatoEntregaComponent } from './Usuarios/formato-entrega/formato-entrega.component';
import { PdfMakeWrapper } from 'pdfmake-wrapper';
import * as pdfFonts from "pdfmake/build/vfs_fonts";
import { FilterPipe } from './pipes/filter.pipe';
PdfMakeWrapper.setFonts(pdfFonts);
/*import { DashboardTipoActivoComponent } from './tipoActivo/dashboard-tipo-activo/dashboard-tipo-activo.component';
import { EditarTipoActivoComponent } from './tipoActivo/editar-tipo-activo/editar-tipo-activo.component';
import { NuevoTipoActivoComponent } from './tipoActivo/nuevo-tipo-activo/nuevo-tipo-activo.component';
import { NuevoActivosComponent } from './Activos/nuevo-activos/nuevo-activos.component';
import { EditarActivosComponent } from './Activos/editar-activos/editar-activos.component';
import { DashboardActivosComponent } from './Activos/dashboard-activos/dashboard-activos.component';
import { DashboardConsumiblesComponent } from './Consumibles/dashboard-consumibles/dashboard-consumibles.component';
import { EditarConsumiblesComponent } from './Consumibles/editar-consumibles/editar-consumibles.component';
import { NuevoConsumiblesComponent } from './Consumibles/nuevo-consumibles/nuevo-consumibles.component';
import { NuevoPerifericosComponent } from './Perifericos/nuevo-perifericos/nuevo-perifericos.component';
import { EditarPerifericosComponent } from './Perifericos/editar-perifericos/editar-perifericos.component';
import { DashboardPerifericosComponent } from './Perifericos/dashboard-perifericos/dashboard-perifericos.component';
import { DashboardUsuariosComponent } from './Usuarios/dashboard-usuarios/dashboard-usuarios.component';
import { EditarUsuariosComponent } from './Usuarios/editar-usuarios/editar-usuarios.component';
import { NuevoUsuariosComponent } from './Usuarios/nuevo-usuarios/nuevo-usuarios.component';*/

@NgModule({
  declarations: [
    AppComponent,
    AppRoutingComponent,
    HeaderComponent,
    FooterComponent,
    AsignacionActivosComponent,
    FormatoEntregaComponent,
    FilterPipe,
    /*DashboardTipoActivoComponent,
    EditarTipoActivoComponent,
    NuevoTipoActivoComponent,
    NuevoActivosComponent,
    EditarActivosComponent,
    DashboardActivosComponent,
    DashboardConsumiblesComponent,
    EditarConsumiblesComponent,
    NuevoConsumiblesComponent,
    NuevoPerifericosComponent,
    EditarPerifericosComponent,
    DashboardPerifericosComponent,
    DashboardUsuariosComponent,
    EditarUsuariosComponent,
    NuevoUsuariosComponent*/
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
import { DashboardTipoActivoComponent } from './tipoActivo/dashboard-tipo-activo/dashboard-tipo-activo.component';
import { EditarTipoActivoComponent } from './tipoActivo/editar-tipo-activo/editar-tipo-activo.component';
import { NuevoTipoActivoComponent } from './tipoActivo/nuevo-tipo-activo/nuevo-tipo-activo.component';
import { DashboardActivosComponent } from './Activos/dashboard-activos/dashboard-activos.component';
import { EditarActivosComponent } from './Activos/editar-activos/editar-activos.component';
import { NuevoActivosComponent } from './Activos/nuevo-activos/nuevo-activos.component';
import { DashboardPerifericosComponent } from './Perifericos/dashboard-perifericos/dashboard-perifericos.component';
import { EditarPerifericosComponent } from './Perifericos/editar-perifericos/editar-perifericos.component';
import { NuevoPerifericosComponent } from './Perifericos/nuevo-perifericos/nuevo-perifericos.component';
import { DashboardConsumiblesComponent } from './Consumibles/dashboard-consumibles/dashboard-consumibles.component';
import { EditarConsumiblesComponent } from './Consumibles/editar-consumibles/editar-consumibles.component';
import { NuevoConsumiblesComponent } from './Consumibles/nuevo-consumibles/nuevo-consumibles.component';
import { DashboardUsuariosComponent } from './Usuarios/dashboard-usuarios/dashboard-usuarios.component';
import { EditarUsuariosComponent } from './Usuarios/editar-usuarios/editar-usuarios.component';
import { NuevoUsuariosComponent } from './Usuarios/nuevo-usuarios/nuevo-usuarios.component';
import { HeaderComponent } from './header/header.component';
import { AsignacionActivosComponent } from './Usuarios/asignacion-activos/asignacion-activos.component';
import { FormatoEntregaComponent } from './Usuarios/formato-entrega/formato-entrega.component';
/*import { LoginComponent } from './vistas/login/login.component';
import { EditarComponent } from './vistas/editar/editar.component';
import { DasboardComponent } from './vistas/dashboard/dashboard.component';
import { NuevoComponent } from './vistas/nuevo/nuevo.component';
import { DashboardActivosComponent} from './activos/dashboard-activos/dashboard-activos.component';
import { EditarActivosComponent } from './activos/editar-activos/editar-activos.component';
import { NuevoActivosComponent } from './activos/nuevo-activos/nuevo-activos.component';
import { DashboardConsumiblesComponent } from './consumibles/dashboard-consumibles/dashboard-consumibles.component';
import { EditarConsumiblesComponent } from './consumibles/editar-consumibles/editar-consumibles.component';
import { NuevoConsumiblesComponent } from './consumibles/nuevo-consumibles/nuevo-consumibles.component';
import { DashboardPerifericosComponent } from './perifericos/dashboard-perifericos/dashboard-perifericos.component';
import { EditarPerifericosComponent } from './perifericos/editar-perifericos/editar-perifericos.component';
import { NuevoPerifericosComponent } from './perifericos/nuevo-perifericos/nuevo-perifericos.component';
import { DashboardUsuariosComponent } from './usuarios/dashboard-usuarios/dashboard-usuarios.component';
import { EditarUsuariosComponent } from './usuarios/editar-usuarios/editar-usuarios.component';
import { NuevoUsuariosComponent } from './usuarios/nuevo-usuarios/nuevo-usuarios.component';*/

const routes: Routes = [
  //Agregar ruta por defecto login
  {path:'',redirectTo:'dashboard_activos', pathMatch:'full'},
  //Agregar path de rutas
  {path:'editar_tipoActivo/:id', component:EditarTipoActivoComponent},
  {path:'dashboard_tipoActivo', component:DashboardTipoActivoComponent},
  {path:'nuevo_tipoActivos', component:NuevoTipoActivoComponent},
  {path:'dashboard_activos', component:DashboardActivosComponent},
  {path:'editar_activos/:id', component:EditarActivosComponent},
  {path:'nuevo_activos', component:NuevoActivosComponent},
  {path:'dashboard_consumibles', component:DashboardConsumiblesComponent},
  {path:'editar_consumibles/:id', component:EditarConsumiblesComponent},
  {path:'nuevo_consumibles', component:NuevoConsumiblesComponent},
  {path:'dashboard_perifericos', component:DashboardPerifericosComponent},
  {path:'editar_perifericos/:id', component:EditarPerifericosComponent},
  {path:'nuevo_perifericos', component:NuevoPerifericosComponent},
  {path:'dashboard_usuarios', component:DashboardUsuariosComponent},
  {path:'editar_usuarios/:id', component:EditarUsuariosComponent},
  {path:'nuevo_usuarios', component:NuevoUsuariosComponent},
  {path:'asignacion_activos/:id', component:AsignacionActivosComponent},
  {path:'formato_entrega/:IdUser/:IdActPrimary/:IdActSp', component:FormatoEntregaComponent},
  {path:'header', component:HeaderComponent},
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }

export const  AppRoutingComponent = [
  EditarTipoActivoComponent, DashboardTipoActivoComponent,NuevoTipoActivoComponent,
  DashboardActivosComponent, EditarActivosComponent, NuevoActivosComponent,
  DashboardConsumiblesComponent, EditarConsumiblesComponent, NuevoConsumiblesComponent,
  DashboardPerifericosComponent, EditarPerifericosComponent, NuevoPerifericosComponent,
  DashboardUsuariosComponent, DashboardUsuariosComponent, NuevoUsuariosComponent, AsignacionActivosComponent,
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

