Google Map integration in Angular using AGM

Table of Contents 
Introduction 
Setting up a basic project structure
Install dependencies 
Setting up @NgModule 
Extending the app Component
Setup the template
Setup the CSS file
Build and Run your application
Github Repository
Conclusion

Introduction

The google map integration in angular allows developers to show locations on google maps and information about location in the content window when we move the cursor over the marker.

Setting up a basic project structure
Create an Angular CLI project
We start by creating a project with angular-cli. If you haven’t installed Angular CLI yet, please run the following command first:

npm install -g @angular/cli

Run the following commands to create a new Angular project with Angular CLI:
ng new angular-google-maps
cd angular-google-maps
Install Dependencies
Install Angular Google Maps (short name: AGM) via the Node Package Manager (NPM). Run the following commands to add it to your new project:

npm install @agm/core
npm i @types/googlemaps@3.39.13

Setting up @NgModule 
Open src/app/app.module.ts and import the AgmCoreModule. You need to provide a Google Maps API key to be able to see a Map. Get an API key here.

import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AgmCoreModule } from '@agm/core';
 
import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
 
@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    AgmCoreModule.forRoot({
      apiKey: ''
    })
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
 


Extending the app Component
Angular CLI already created an app component that we’ll now use to create our first google map. We have added markers array, set zoom level, default latitude, longitude and click marker event in the app component. Open the file src/app/app.component.ts and modify it like below:
import { Component } from '@angular/core';
 
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent  {
  // google maps zoom level
  zoom: number = 8;
 
  // initial center position for the map
  lat: number = 51.673858;
  lng: number = 7.815982;
 
  clickedMarker(label: string, index: number) {
    console.log(`clicked the marker: ${label || index}`)
  }
 
  markers = [
      {
          lat: 51.673858,
          lng: 7.815982,
          label: "A",
          draggable: true
      },
      {
          lat: 51.373858,
          lng: 7.215982,
          label: "B",
          draggable: false
      },
      {
          lat: 51.723858,
          lng: 7.895982,
          label: "C",
          draggable: true
      }
  ]
}


Setup the template
Open the file src/app/app.component.html and paste the following content:
<h1>Angular Google Maps (AGM) Demo</h1>
 
<agm-map
  [latitude]="lat"
  [longitude]="lng"
  [zoom]="zoom"
  [disableDefaultUI]="false"   >
 
  <agm-marker
      *ngFor="let m of markers; let i = index"
      (markerClick)="clickedMarker(m.label, i)"
      [latitude]="m.lat"
      [longitude]="m.lng"
      [label]="m.label"
      [markerDraggable]="m.draggable">
     
    <agm-info-window>
      <strong>Label: {{m.label}}</strong><br/>
      <strong>Latitude: {{m.lat}}</strong><br/>
      <strong>Longitude: {{m.lng}}</strong>
    </agm-info-window>
   
  </agm-marker>
 
</agm-map>

Setup the CSS file
Open the file src/app/app.component.css and paste the following content:
agm-map {
    height: 500px;
}
Build and Run your application
Run the below command in the project root folder:

npm start

Then, open the following URL in your browser: http://localhost:4200

When everything works as expected, you should see your first Google Map created with AGM
