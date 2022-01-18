# cofiguredata

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
