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