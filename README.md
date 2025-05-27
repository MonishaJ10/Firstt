Step 1: Create a New Angular Project (No module.ts)
Since you mentioned module.ts won't be present (implying possibly a standalone component structure in Angular 15+), we will proceed using standalone components only.

bash
Copy
Edit
ng new system-setup --standalone
cd system-setup
Choose standalone components when prompted (or use --standalone).

✅ Step 2: Install Required Dependencies
Install Font Awesome and Tailwind CSS.

2.1 Install Font Awesome
bash
Copy
Edit
npm install @fortawesome/fontawesome-free
Add to angular.json:

json
Copy
Edit
"styles": [
  "src/styles.css",
  "node_modules/@fortawesome/fontawesome-free/css/all.min.css"
]
2.2 Setup Tailwind CSS
Follow the Tailwind Angular setup guide or do:

bash
Copy
Edit
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init
Update tailwind.config.js:

js
Copy
Edit
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./src/**/*.{html,ts}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
Update src/styles.css:

css
Copy
Edit
@tailwind base;
@tailwind components;
@tailwind utilities;
✅ Step 3: Generate Components
bash
Copy
Edit
ng generate component components/header --standalone --flat --skip-tests
ng generate component components/sidebar --standalone --flat --skip-tests
ng generate component pages/accounting-period-groups --standalone --flat --skip-tests
ng generate component pages/manage-company --standalone --flat --skip-tests
ng generate component pages/context-type --standalone --flat --skip-tests
ng generate component pages/reference-data --standalone --flat --skip-tests
✅ Step 4: Setup Routing
Update main.ts and create your own root component for bootstrapping.

4.1 Create App Component (src/app/app.component.ts):
ts
Copy
Edit
import { Component } from '@angular/core';
import { RouterModule } from '@angular/router';
import { HeaderComponent } from './components/header';
import { SidebarComponent } from './components/sidebar';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [RouterModule, HeaderComponent, SidebarComponent],
  template: `
    <div class="h-screen flex flex-col bg-[#007a9e] font-sans text-[13px] text-white">
      <app-header></app-header>
      <div class="flex flex-grow">
        <app-sidebar></app-sidebar>
        <div class="flex-grow bg-[#f5f5f5] text-[#333] overflow-y-auto">
          <router-outlet></router-outlet>
        </div>
      </div>
    `
})
export class AppComponent {}
4.2 Update main.ts to use AppComponent
ts
Copy
Edit
import { bootstrapApplication } from '@angular/platform-browser';
import { AppComponent } from './app/app.component';
import { provideRouter } from '@angular/router';
import { routes } from './app/app.routes';

bootstrapApplication(AppComponent, {
  providers: [provideRouter(routes)],
});
4.3 Create app.routes.ts
ts
Copy
Edit
import { Routes } from '@angular/router';
import { AccountingPeriodGroupsComponent } from './pages/accounting-period-groups';
import { ManageCompanyComponent } from './pages/manage-company';
import { ContextTypeComponent } from './pages/context-type';
import { ReferenceDataComponent } from './pages/reference-data';

export const routes: Routes = [
  { path: '', redirectTo: 'accounting-period-groups', pathMatch: 'full' },
  { path: 'accounting-period-groups', component: AccountingPeriodGroupsComponent },
  { path: 'manage-company', component: ManageCompanyComponent },
  { path: 'context-type', component: ContextTypeComponent },
  { path: 'reference-data', component: ReferenceDataComponent }
];
✅ Step 5: Component HTML and Logic
5.1 header.component.ts
Copy the top bar code here and replace any button navigation with [routerLink].

Example:

html
Copy
Edit
<header class="flex items-center h-12 px-3 bg-[#007a9e] border-b border-[#005f7a]">
  <button class="mr-3 text-white text-lg">
    <i class="fas fa-bars"></i>
  </button>
  <button [routerLink]="['/']" class="mr-3 text-white text-lg">
    <i class="fas fa-home"></i>
  </button>
  <div class="flex items-center bg-[#008db8] rounded-sm px-3 py-1 text-[13px] font-semibold select-text">
    <span>System Setup</span>
    <button class="ml-2 text-white hover:text-[#007a9e]">
      <i class="fas fa-times"></i>
    </button>
  </div>
  <div class="flex-grow"></div>
  <button class="text-white text-lg">
    <i class="fas fa-search"></i>
  </button>
</header>
5.2 sidebar.component.ts
Include all left nav links with [routerLink]:

html

<nav class="flex flex-col w-56 bg-gradient-to-b from-[#005f7a] to-[#004d63] border-r border-[#004d63] text-[13px] overflow-y-auto scrollbar-thin">
  <a routerLink="/manage-company" class="flex items-center gap-2 px-4 py-3 hover:bg-[#007a9e] border-b border-[#004d63]">
    <i class="fas fa-university text-white"></i>
    <span>Manage Company</span>
  </a>

  <div class="border-b border-[#004d63]">
    <button class="flex items-center gap-2 w-full px-4 py-3 hover:bg-[#007a9e]">
      <i class="fas fa-file-alt text-white"></i>
      <span>Recon Master</span>
    </button>
  </div>

  <a routerLink="/context-type" class="flex items-center gap-2 px-4 py-3 hover:bg-[#007a9e] border-b border-[#004d63]">
    <i class="fas fa-cog text-white"></i>
    <span>Context Type</span>
  </a>

  <a routerLink="/reference-data" class="flex items-center gap-2 px-4 py-3 hover:bg-[#007a9e] border-b border-[#004d63]">
    <i class="fas fa-database text-white"></i>
    <span>Reference Data</span>
  </a>
</nav>
✅ Step 6: Content Component (Example: accounting-period-groups.component.ts)
Use your original main content and move relevant section to this page:

html

<!-- Accounting Period Group Page -->
<div class="p-4 text-[11px] text-[#666]">
  <div class="mb-2 font-semibold text-[12px] text-[#666]">Accounting Periods</div>
  <div class="pt-20 text-center text-[11px] text-[#999] select-text">
    Click on &gt;&gt; to view the accounting periods.
  </div>
</div>
Repeat for each other component by copying the respective section.


WITH NORMAL CSS
📁 Step 2: Generate Components

Generate the necessary components using Angular CLI:

ng generate component components/header --standalone
ng generate component components/sidebar --standalone
ng generate component pages/accounting-period-groups --standalone
ng generate component pages/manage-company --standalone
ng generate component pages/context-type --standalone
ng generate component pages/reference-data --standalone


---

🧭 Step 3: Set Up Routing

3.1: Define Routes

Create a src/app/app.routes.ts file:

import { Routes } from '@angular/router';
import { AccountingPeriodGroupsComponent } from './pages/accounting-period-groups/accounting-period-groups.component';
import { ManageCompanyComponent } from './pages/manage-company/manage-company.component';
import { ContextTypeComponent } from './pages/context-type/context-type.component';
import { ReferenceDataComponent } from './pages/reference-data/reference-data.component';

export const routes: Routes = [
  { path: '', redirectTo: 'accounting-period-groups', pathMatch: 'full' },
  { path: 'accounting-period-groups', component: AccountingPeriodGroupsComponent },
  { path: 'manage-company', component: ManageCompanyComponent },
  { path: 'context-type', component: ContextTypeComponent },
  { path: 'reference-data', component: ReferenceDataComponent },
];

3.2: Update main.ts

Modify src/main.ts to bootstrap the application with routing:

import { bootstrapApplication } from '@angular/platform-browser';
import { AppComponent } from './app/app.component';
import { provideRouter } from '@angular/router';
import { routes } from './app/app.routes';

bootstrapApplication(AppComponent, {
  providers: [provideRouter(routes)],
});


---

🧱 Step 4: Create the Root Component

Create src/app/app.component.ts:

import { Component } from '@angular/core';
import { RouterOutlet } from '@angular/router';
import { HeaderComponent } from './components/header/header.component';
import { SidebarComponent } from './components/sidebar/sidebar.component';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [RouterOutlet, HeaderComponent, SidebarComponent],
  template: `
    <div class="app-container">
      <app-header></app-header>
      <div class="main-content">
        <app-sidebar></app-sidebar>
        <div class="content-area">
          <router-outlet></router-outlet>
        </div>
      </div>
    </div>
  `,
  styles: [`
    .app-container {
      display: flex;
      flex-direction: column;
      height: 100vh;
      font-family: sans-serif;
      font-size: 13px;
      color: #fff;
      background-color: #007a9e;
    }
    .main-content {
      display: flex;
      flex: 1;
    }
    .content-area {
      flex: 1;
      background-color: #f5f5f5;
      color: #333;
      overflow-y: auto;
    }
  `]
})
export class AppComponent {}


---

🧩 Step 5: Implement Header Component

Update src/app/components/header/header.component.ts:

import { Component } from '@angular/core';

@Component({
  selector: 'app-header',
  standalone: true,
  template: `
    <header class="header">
      <button aria-label="Menu" class="icon-button">
        <i class="fas fa-bars"></i>
      </button>
      <button aria-label="Home" class="icon-button">
        <i class="fas fa-home"></i>
      </button>
      <div class="title-bar">
        <span>System Setup</span>
        <button aria-label="Close tab" class="close-button">
          <i class="fas fa-times"></i>
        </button>
      </div>
      <div class="spacer"></div>
      <button aria-label="Search" class="icon-button">
        <i class="fas fa-search"></i>
      </button>
    </header>
  `,
  styles: [`
    .header {
      display: flex;
      align-items: center;
      height: 48px;
      padding: 0 12px;
      background-color: #007a9e;
      border-bottom: 1px solid #005f7a;
    }
    .icon-button {
      margin-right: 12px;
      color: #fff;
      font-size: 18px;
      background: none;
      border: none;
      cursor: pointer;
    }
    .title-bar {
      display: flex;
      align-items: center;
      background-color: #008db8;
      border-radius: 4px;
      padding: 4px 12px;
      font-weight: bold;
    }
    .close-button {
      margin-left: 8px;
      color: #fff;
      background: none;
      border: none;
      cursor: pointer;
    }
    .spacer {
      flex-grow: 1;
    }
  `]
})
export class HeaderComponent {}


---

📚 Step 6: Implement Sidebar Component

Update src/app/components/sidebar/sidebar.component.ts:

import { Component } from '@angular/core';
import { RouterModule } from '@angular/router';

@Component({
  selector: 'app-sidebar',
  standalone: true,
  imports: [RouterModule],
  template: `
    <nav class="sidebar">
      <a routerLink="/manage-company" class="nav-link">
        <i class="fas fa-university"></i>
        <span>Manage Company</span>
      </a>
      <div class="nav-section">
        <button class="nav-button">
          <i class="fas fa-file-alt"></i>
          <span>Recon Master</span>
        </button>
      </div>
      <a routerLink="/context-type" class="nav-link">
        <i class="fas fa-cog"></i>
        <span>Context Type</span>
      </a>
      <a routerLink="/reference-data" class="nav-link">
        <i class="fas fa-database"></i>
        <span>Reference Data</span>
      </a>
    </nav>
  `,
  styles: [`
    .sidebar {
      width: 224px;
      background: linear-gradient(to bottom, #005f7a, #004d63);
      border-right: 1px solid #004d63;
      font-size: 13px;
      overflow-y: auto;
    }
    .nav-link, .nav-button {
      display: flex;
      align-items: center;
      gap: 8px;
      padding: 12px 16px;
      color: #fff;
      text-decoration: none;
      border-bottom: 1px solid #004d63;
      background: none;
      border: none;
      width: 100%;
      text-align: left;
      cursor: pointer;
    }
    .nav-link:hover, .nav-button:hover {
      background-color: #007a9e;
    }
    .nav-section {
      border-bottom: 1px solid #004d63;
    }
  `]
})
export class SidebarComponent {}


---

📄 Step 7: Implement Page Components

7.1: Accounting Period Groups

Update src/app/pages/accounting-period-groups/accounting-period-groups.component.ts:

import { Component } from '@angular/core';

@Component({
  selector: 'app-accounting-period-groups',
  standalone: true,
  template: `
    <div class="page-header">
      <span>Accounting Period Groups</span>
      <button aria-label="Close tab" class="close-button">
        <i class="fas fa-times"></i>
      </button>
    </div>
    <div class="page-content">
      <div class="left-panel">
        <div class="button-group">
          <button aria-label="Add" class="action-button">
            <i class="fas fa-plus"></i>
          </button>
          <button aria-label="Delete" class="action-button">
            <i class="fas fa-trash-alt"></i>
          </button>
          <button aria-label="Refresh" class="action-button">
            <i class="fas fa-sync-alt"></i>
          </button>
        </div>
        <table class="data-table">
          <thead>
            <tr>
              <th>Name</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>No Rows To Show</td>
            </tr>
          </tbody>
        </table>
      </div>
      <div class="right-panel">
        <div class="section-title">Accounting Periods</div>
        <div class="placeholder-text">
          Click on &gt;&gt; to view the accounting periods.
        </div>
      </div>
    </div>
  `,
  styles: [`
    .page-header {
      display: flex;
      align-items: center;
      height: 40px;
      padding: 0 16px;
      border-bottom: 1px solid #008db8;
      font-weight: bold;
      color: #008db8;
    }
    .close-button {
      margin-left: 8px;
      color: #008db8;
      background: none;
      border: none;
      cursor: pointer;
    }
    .page-content {
      display: flex;
      height: calc(100vh - 88px); /* Adjust based on header and page-header heights */
    }
    .left-panel {
      width: 256px;
      border-right: 1px solid #d1d1d1;
      display: flex;
      flex-direction: column;
    }
    .button-group {
      display: flex;
      gap: 8px;
      padding: 8px;
      border-bottom: 1px solid #d1d1d1;
      background-color: #f9f9f9;
    }
    .action-button {
      width: 28px;
      height: 28px;
      border: 1px solid #d1d1d1;
      border-radius: 4px;
      background-color:0

