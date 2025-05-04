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




