1. BACKEND: SPRING BOOT (WITHOUT Spring Initializer)
📁 Folder Structure (create manually in IntelliJ):
SocratesNextGenBackend/
├── src/
│   └── main/
│       ├── java/
│       │   └── com/
│       │       └── socrates/
│       │           └── nextgen/
│       │               ├── controller/
│       │               │   └── CSVController.java
│       │               ├── model/
│       │               │   └── DataRecord.java
│       │               ├── repository/
│       │               │   └── DataRecordRepository.java
│       │               └── SocratesNextGenApplication.java
│       └── resources/
│           ├── application.properties


 Why create these files/folders:
File/Folder	Purpose
CSVController.java	              Logic to upload & preview CSV
DataRecord.java	                  Entity class for Oracle DB
DataRecordRepository.java	        Interface to talk to Oracle
application.properties	          DB config (Oracle)
SocratesNextGenApplication.java	  Main Spring Boot entry point

 SocratesNextGenApplication.java
package com.socrates.nextgen;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class SocratesNextGenApplication {
    public static void main(String[] args) {
        SpringApplication.run(SocratesNextGenApplication.class, args);
    }
}

CSVController.java
package com.socrates.nextgen.controller;

import org.springframework.web.bind.annotation.*;
import org.springframework.web.multipart.MultipartFile;
import org.springframework.http.ResponseEntity;
import org.springframework.http.HttpStatus;

import java.io.*;
import java.util.*;

@RestController
@RequestMapping("/api/csv")
@CrossOrigin(origins = "*")
public class CSVController {

    @PostMapping("/upload")
    public ResponseEntity<Map<String, List<List<String>>>> upload(
            @RequestParam("file1") MultipartFile file1,
            @RequestParam("file2") MultipartFile file2) throws IOException {

        Map<String, List<List<String>>> previewData = new HashMap<>();
        previewData.put("file1", getPreview(file1));
        previewData.put("file2", getPreview(file2));

        return ResponseEntity.ok(previewData);
    }

    private List<List<String>> getPreview(MultipartFile file) throws IOException {
        List<List<String>> rows = new ArrayList<>();
        try (BufferedReader br = new BufferedReader(new InputStreamReader(file.getInputStream()))) {
            String line;
            int count = 0;
            while ((line = br.readLine()) != null && count < 5) {
                String[] parts = line.split(",");
                rows.add(Arrays.asList(parts));
                count++;
            }
        }
        return rows;
    }
}


application.properties
spring.datasource.url=jdbc:oracle:thin:@localhost:1521:xe
spring.datasource.username=YOUR_USERNAME
spring.datasource.password=YOUR_PASSWORD
spring.datasource.driver-class-name=oracle.jdbc.OracleDriver

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true

if You Don’t Add Dependencies via Spring Initializr…
Add them manually in pom.xml:
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>com.oracle.database.jdbc</groupId>
        <artifactId>ojdbc8</artifactId>
        <version>19.3.0.0</version>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
</dependencies>

 FRONTEND: Angular App (Green + White)
📁 Folder Structure
socrates-nextgen-frontend/
├── src/
│   └── app/
│       ├── upload/
│       │   ├── upload.component.ts
│       │   ├── upload.component.html
│       │   └── upload.component.css
│       └── app.module.ts
└── angular.json

ng new socrates-nextgen-frontend
cd socrates-nextgen-frontend
ng generate component upload

upload.component.ts
import { Component } from '@angular/core';
import { HttpClient } from '@angular/common/http';

@Component({
  selector: 'app-upload',
  templateUrl: './upload.component.html',
  styleUrls: ['./upload.component.css']
})
export class UploadComponent {
  file1?: File;
  file2?: File;
  previewFile1: string[][] = [];
  previewFile2: string[][] = [];

  constructor(private http: HttpClient) {}

  onFile1Change(event: any) {
    this.file1 = event.target.files[0];
  }

  onFile2Change(event: any) {
    this.file2 = event.target.files[0];
  }

  upload() {
    const formData = new FormData();
    formData.append('file1', this.file1!);
    formData.append('file2', this.file2!);

    this.http.post<any>('http://localhost:8080/api/csv/upload', formData)
      .subscribe(data => {
        this.previewFile1 = data.file1;
        this.previewFile2 = data.file2;
      });
  }
}

upload.component.html
<h2>Socrates NextGen File Upload</h2>

<label>Select File 1: <input type="file" (change)="onFile1Change($event)"></label><br><br>
<label>Select File 2: <input type="file" (change)="onFile2Change($event)"></label><br><br>
<button (click)="upload()">Upload</button>

<div *ngIf="previewFile1.length">
  <h3>Preview of File 1</h3>
  <table>
    <tr *ngFor="let row of previewFile1">
      <td *ngFor="let cell of row">{{ cell }}</td>
    </tr>
  </table>
</div>

<div *ngIf="previewFile2.length">
  <h3>Preview of File 2</h3>
  <table>
    <tr *ngFor="let row of previewFile2">
      <td *ngFor="let cell of row">{{ cell }}</td>
    </tr>
  </table>
</div>

upload.component.css
h2, h3 {
  color: #007A33; /* BNP Paribas green */
}

table {
  border-collapse: collapse;
  margin-top: 10px;
  background-color: white;
  color: black;
}

td {
  border: 1px solid #007A33;
  padding: 5px 10px;
}

First, generate your components:
In terminal (inside your Angular project):
ng generate component upload
ng generate component review
ng generate component result

app.module.ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { HttpClientModule } from '@angular/common/http';
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { MatButtonModule } from '@angular/material/button';
import { MatCardModule } from '@angular/material/card';
import { MatTableModule } from '@angular/material/table';
import { MatInputModule } from '@angular/material/input';
import { MatIconModule } from '@angular/material/icon';
import { FormsModule } from '@angular/forms';

import { AppComponent } from './app.component';
import { UploadComponent } from './upload/upload.component';
import { ReviewComponent } from './review/review.component';
import { ResultComponent } from './result/result.component';

@NgModule({
  declarations: [
    AppComponent,
    UploadComponent,
    ReviewComponent,
    ResultComponent
  ],
  imports: [
    BrowserModule,
    HttpClientModule,
    BrowserAnimationsModule,
    FormsModule,
    MatButtonModule,
    MatCardModule,
    MatTableModule,
    MatInputModule,
    MatIconModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }

To Run the Full App:
Start Spring Boot server from IntelliJ (SocratesNextGenApplication)

Run Angular:
cd socrates-nextgen-frontend
ng serve
Visit: http://localhost:4200








npm install primeng@^16.0.0 primeicons@^6.0.0 --legacy-peer-deps
npm install ag-grid-angular@^31.0.0 ag-grid-community@^31.0.0 --legacy-peer-deps
npm install @angular/material@^17.0.0 @angular/cdk@^17.0.0 --legacy-peer-deps

import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { MatInputModule } from '@angular/material/input';
import { MatButtonModule } from '@angular/material/button';
import { MatFormFieldModule } from '@angular/material/form-field';
import { FormsModule, ReactiveFormsModule } from '@angular/forms';
import { PrimeIconsModule } from 'primeng/api';
import { PanelModule } from 'primeng/panel';

@NgModule({
  declarations: [...],
  imports: [
    BrowserModule,
    BrowserAnimationsModule,
    FormsModule,
    ReactiveFormsModule,
    MatInputModule,
    MatButtonModule,
    MatFormFieldModule,
    PanelModule
  ],
  bootstrap: [AppComponent]
})
export class AppModule { }


main.ts
import { bootstrapApplication } from '@angular/platform-browser';
import { AppComponent } from './app/app.component';
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { provideAnimations } from '@angular/platform-browser/animations';

bootstrapApplication(AppComponent, {
  providers: [provideAnimations()]
});


app.component.ts
import { Component } from '@angular/core';
import { FormsModule, ReactiveFormsModule } from '@angular/forms';
import { MatInputModule } from '@angular/material/input';
import { MatButtonModule } from '@angular/material/button';
import { MatFormFieldModule } from '@angular/material/form-field';
import { CommonModule } from '@angular/common';
import { PanelModule } from 'primeng/panel';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [
    CommonModule,
    FormsModule,
    ReactiveFormsModule,
    MatInputModule,
    MatButtonModule,
    MatFormFieldModule,
    PanelModule
  ],
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  title = 'NextGen-Recon';
}

%;
}

app.comp.html
<div class="container">
  <!-- Header -->
  <div class="header">
    <img src="assets/bnp-logo.png" alt="BNP Logo" class="logo" />
    <h1 class="title">NextGen Recon</h1>
  </div>

  <!-- Main Content -->
  <div class="main-content">
    <!-- Left Side Boxes -->
    <div class="left-column">
      <div class="content-box">Hyperlinks</div>
      <div class="content-box">Content / Hyperlinks</div>
    </div>

    <!-- Login Box -->
    <div class="login-box">
      <h2>Login</h2>
      <p class="subhead">Reconciliation</p>
      <p class="subhead">Trade Matching</p>

      <form (ngSubmit)="onSubmit()" #loginForm="ngForm" novalidate>
        <mat-form-field appearance="fill">
          <input matInput placeholder="UID" name="uid" [(ngModel)]="uid" required />
        </mat-form-field>
        <div *ngIf="showUidError" class="error-msg">Enter your UID</div>

        <mat-form-field appearance="fill">
          <input matInput type="password" placeholder="Password" name="password" [(ngModel)]="password" required />
        </mat-form-field>

        <button mat-raised-button color="primary" class="login-button" type="submit">Submit</button>
        <div class="or-line">or</div>
        <button mat-stroked-button color="accent" class="sso-button">Login with SSO</button>
      </form>
    </div>
  </div>
</div>

app.comp.css
:host {
  display: block;
  background: #f4fef6;
  font-family: 'Segoe UI', sans-serif;
  padding: 30px;
}

/* Header */
.header {
  display: flex;
  align-items: center;
  gap: 15px;
  margin-bottom: 30px;
}

.logo {
  width: 50px;
  height: 50px;
}

.title {
  font-size: 2rem;
  font-weight: bold;
  color: #2e7d32;
}

/* Main Layout */
.main-content {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
}

.left-column {
  display: flex;
  flex-direction: column;
  gap: 20px;
  flex: 1;
  max-width: 600px;
}

.content-box {
  background: #ffecec;
  padding: 20px;
  border-radius: 12px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  font-size: 1.1rem;
  transition: all 0.3s;
}

.content-box:hover {
  box-shadow: 0 6px 16px rgba(0, 0, 0, 0.2);
}

/* Login Box */
.login-box {
  width: 320px;
  background: linear-gradient(to bottom, #2e7d32, #1b5e20);
  color: white;
  padding: 25px;
  border-radius: 20px;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3);
}

.login-box h2 {
  text-align: center;
  margin-bottom: 10px;
}

.subhead {
  text-align: center;
  font-size: 0.9rem;
  margin-bottom: 10px;
  opacity: 0.85;
}

/* Input & Buttons */
mat-form-field {
  width: 100%;
  background-color: white;
  border-radius: 4px;
  margin-bottom: 10px;
}

input {
  color: black;
}

.login-button,
.sso-button {
  width: 100%;
  font-weight: bold;
  margin-top: 10px;
  border-radius: 6px;
}

.login-button:hover,
.sso-button:hover {
  transform: scale(1.02);
  box-shadow: 0 4px 12px rgba(255, 255, 255, 0.3);
}

/* Error Message */
.error-msg {
  color: red;
  font-size: 0.9rem;
  margin-top: -8px;
  margin-bottom: 10px;
}

.or-line {
  text-align: center;
  margin: 10px 0;
  font-size: 0.85rem;
  color: #ccc;
}



  import { Component } from '@angular/core';
import { CommonModule } from '@angular/common';
import { FormsModule } from '@angular/forms';
import { MatFormFieldModule } from '@angular/material/form-field';
import { MatInputModule } from '@angular/material/input';
import { MatButtonModule } from '@angular/material/button';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css'],
  standalone: true,
  imports: [
    CommonModule,
    FormsModule,
    MatFormFieldModule,
    MatInputModule,
    MatButtonModule
  ]
})
export class AppComponent {
  uid: string = '';
  password: string = '';
  showUidError = false;

  onSubmit() {
    this.showUidError = this.uid.trim() === '';
    if (!this.showUidError) {
      alert('Form submitted!');
    }
  }
}