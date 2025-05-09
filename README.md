
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { FormsModule } from '@angular/forms';

import { AppComponent } from './app.component';

// Angular Material Modules
import { MatFormFieldModule } from '@angular/material/form-field';
import { MatInputModule } from '@angular/material/input';
import { MatButtonModule } from '@angular/material/button';

@NgModule({
  declarations: [AppComponent],
  imports: [
    BrowserModule,
    BrowserAnimationsModule,
    FormsModule,
    MatFormFieldModule,
    MatInputModule,
    MatButtonModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule {}



app.comp.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  username = '';
  password = '';

  onLogin() {
    console.log('Username:', this.username);
    console.log('Password:', this.password);
    alert(`Welcome, ${this.username}`);
  }

  onSSOLogin() {
    alert('SSO Login triggered');
  }
}

app.comp.html
<!-- Header -->
<div class="logo-title">
  <img src="assets/bnp-logo.png" class="logo" alt="BNP Logo" />
  <h1 class="animated-title">NextGen-Recon</h1>
</div>

<!-- Content Layout -->
<div class="main-container">
  <!-- Box 1 -->
  <div class="box green-box">
    <h2>About NextGen-Recon</h2>
    <p>This platform simplifies your reconnaissance efforts with smart automation and visual insights.</p>
  </div>

  <!-- Box 2 -->
  <div class="box green-box">
    <h2>Video Tutorials</h2>
    <div class="mini-box">Intro to Recon</div>
    <div class="mini-box">Getting Started</div>
    <div class="mini-box">Advanced Features</div>
  </div>

  <!-- Box 3 - Login -->
  <div class="box white-box">
    <h2>Login</h2>

    <mat-form-field appearance="outline" class="full-width">
      <mat-label>Username</mat-label>
      <input matInput [(ngModel)]="username">
    </mat-form-field>

    <mat-form-field appearance="outline" class="full-width">
      <mat-label>Password</mat-label>
      <input matInput type="password" [(ngModel)]="password">
    </mat-form-field>

    <button mat-raised-button color="primary" class="full-width" (click)="onLogin()">Submit</button>
    <button mat-stroked-button color="accent" class="full-width" (click)="onSSOLogin()">Login with SSO</button>
  </div>
</div>

app.comp.css
/* Base Theme */
body {
  margin: 0;
  background-color: white;
  font-family: 'Segoe UI', sans-serif;
}

/* Logo and Title */
.logo-title {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 30px 0 10px 0;
  animation: slideDown 1s ease-out;
}

.logo {
  width: 50px;
  margin-right: 10px;
}

.animated-title {
  font-size: 2.5rem;
  color: green;
  font-weight: 600;
}

/* Animation */
@keyframes slideDown {
  from { transform: translateY(-60px); opacity: 0; }
  to { transform: translateY(0); opacity: 1; }
}

/* Layout */
.main-container {
  display: flex;
  justify-content: center;
  gap: 30px;
  padding: 40px 20px;
  flex-wrap: wrap;
}

/* Boxes */
.box {
  border-radius: 15px;
  padding: 25px;
  width: 300px;
  box-shadow: 0 6px 12px rgba(0,0,0,0.15);
}

/* Color Variants */
.green-box {
  background-color: #a5d6a7;
  color: #1b5e20;
}

.white-box {
  background-color: #fff;
  color: #2e7d32;
}

/* Tutorials */
.mini-box {
  background: #e8f5e9;
  margin: 8px 0;
  padding: 12px;
  border-radius: 8px;
  font-weight: 500;
  box-shadow: inset 0 1px 3px rgba(0,0,0,0.1);
}

/* Material Fields */
.full-width {
  width: 100%;
  margin-bottom: 15px;
}

main.ts
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';
import { AppModule } from './app/app.module';

platformBrowserDynamic().bootstrapModule(AppModule)
  .catch(err => console.error(err));




import { Component } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { MatFormFieldModule } from '@angular/material/form-field';
import { MatInputModule } from '@angular/material/input';
import { MatButtonModule } from '@angular/material/button';
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { CommonModule } from '@angular/common';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [
    CommonModule,
    BrowserAnimationsModule,
    FormsModule,
    MatFormFieldModule,
    MatInputModule,
    MatButtonModule
  ],
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  username = '';
  password = '';

  login() {
    console.log('Username:', this.username);
    console.log('Password:', this.password);
  }

  loginSSO() {
    console.log('Login with SSO');
  }
}


import { bootstrapApplication } from '@angular/platform-browser';
import { AppComponent } from './app/app.component';

bootstrapApplication(AppComponent)
  .catch(err => console.error(err));