C:\Users\jmoni\v1\src\app\header
HEADER.COMP.CSS
 .header {
      background: #2c3e50;
      color: white;
      padding: 10px 20px;
      display: flex;
      align-items: center;
      gap: 20px;
    }
    i {
      cursor: pointer;
      font-size: 20px;
    }
    
button {
  background: none;
  border: none;
  color: white;
  font-size: 24px;
  cursor: pointer;
}

button:hover {
  color: #4db8ff;
}

.toggle-btn {
  background: none;
  border: none;
  color: white;
  font-size: 24px;
  cursor: pointer;
}

.toggle-btn:hover {
  color: #4db8ff;
}

.opened-module {
  margin-left: 20px;
  font-weight: 600;
  font-size: 18px;
  display: flex;
  align-items: center;
  gap: 10px;
  user-select: none;
}

.close-icon {
  cursor: pointer;
  font-size: 16px;
  color: #bbb;
}

.close-icon:hover {
  color: #ff4d4d;
}

HEADER.COMP.HTML
<header class="header">
<button (click)="toggleSidebar()">
  <i class="fa fa-bars"></i> 
</button>

      <i class="fas fa-home"></i>
      <i class="fas fa-folder"></i>

      <div *ngIf="openedModule" class="opened-module">
    {{ openedModule }}
    <i class="fas fa-times close-icon" (click)="closeOpenedModule($event)"></i>
  </div>
    </header>

  HEADER.COMP.TS
  import { Component,Input, Output, EventEmitter } from '@angular/core';
import { Router } from '@angular/router';
import { CommonModule } from '@angular/common';

@Component({
  selector: 'app-header',
  imports : [CommonModule],
  templateUrl: './header.component.html',
  styleUrls: ['./header.component.css']
})

export class HeaderComponent {
  @Input() openedModule: string | null = null;
  @Output() toggle = new EventEmitter<void>(); 
  @Output() closeModule = new EventEmitter<void>();
  toggleSidebar() {
    this.toggle.emit(); 
  }
   closeOpenedModule(event: MouseEvent) {
    event.stopPropagation(); // prevent triggering toggleSidebar
    this.closeModule.emit();
  }
}

C:\Users\jmoni\v1\src\app\pages
ADMIN

BLANK
blank.comp.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-blank',
  standalone: true,
  template: ``, // This will render nothing
  imports: []
})
export class BlankComponent {}

INVENTORY CONFIGURATION

INVENTORY SIBEBAR 
inventory-sidebar.component.css
 .sidebar {
      width: 220px;
      background-color: #34495e;
      color: white;
      height: 100vh;
      padding-top: 20px;
    }
    ul {
      list-style: none;
      padding: 0;
    }
    li {
      padding: 15px 20px;
      cursor: pointer;
    }
    .active {
      background-color: #2c3e50;
      font-weight: bold;
    }

.sidebar ul li {
  padding: 10px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.sidebar ul li:hover {
  background-color: #638fda;
}

.sidebar ul li.active {
  background-color: #5787ba;
  color: white;
  font-weight: bold;
}

.sidebar ul li.active i {
  color: white;
}

inventory-sidebar.component.html
<nav class="sidebar">
  <ul>
  <li (click)="goTo('manage-dashboard')">
    <i class="fas fa-chart-bar"></i> Manage Dashboard
  </li>
  <li (click)="goTo('recon-view-manager')">
    <i class="fas fa-eye"></i> Recon View Manager
  </li>
  <li (click)="goTo('model-categories')">
    <i class="fas fa-layer-group"></i> Model Categories
  </li>
</ul>
</nav>

inventory-sidebar.component.ts
import { Component, EventEmitter, Output } from '@angular/core';

@Component({
  selector: 'app-inventory-sidebar',
  imports: [],
  templateUrl: './inventory-sidebar.component.html',
  styleUrl: './inventory-sidebar.component.css'
})
export class InventorySidebarComponent {
  @Output() navigate = new EventEmitter<string>();

  goTo(route: string) {
    this.navigate.emit(route);
  }
}



MANAGE DASHBOARD
MODEL CATEGORIES
RECON VIEW MANAGER

SIBEBAR
sidebar.component.css
 .sidebar {
      width: 220px;
      background-color: #34495e;
      color: white;
      height: 100vh;
      padding-top: 20px;
    }
    ul {
      list-style: none;
      padding: 0;
    }
    li {
      padding: 15px 20px;
      cursor: pointer;
    }
    .active {
      background-color: #2c3e50;
      font-weight: bold;
    }


  .sidebar ul li {
  padding: 10px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.sidebar ul li:hover {
  background-color: #638fda;
}

.sidebar ul li.active {
  background-color: #5787ba;
  color: white;
  font-weight: bold;
}

.sidebar ul li.active i {
  color: white;
}

sidebar.component.html
<!-- <nav class="sidebar">
      <ul>
        <li routerLink="/inventory" routerLinkActive="active">Inventory Configuration</li>
        <li routerLink="/system-setup" routerLinkActive="active">System Setup</li>
        <li routerLink="/admin" routerLinkActive="active">Admin</li>
        <li routerLink="/import-export" routerLinkActive="active">Import-export Manager</li>
      </ul>
    </nav> -->

<nav class="sidebar">
  <ul>
    <li (click)="selectModule('Inventory Configuration')">
      <i class="fas fa-box"></i> Inventory Configuration
    </li>
    <li (click)="selectModule('System Setup')">
      <i class="fas fa-cogs"></i> System Setup
    </li>
    <li (click)="selectModule('Admin')">
      <i class="fas fa-user-cog"></i> Admin
    </li>
    <li (click)="selectModule('Import-Export Manager')">
      <i class="fas fa-file-import"></i> Import-Export Manager
    </li>
  </ul>
</nav>

sidebar.component.ts
import { Component,EventEmitter,Input, Output } from '@angular/core';
import { RouterModule } from '@angular/router';
import { CommonModule } from '@angular/common';

@Component({
  selector: 'app-sidebar',
  imports: [CommonModule, RouterModule],
  templateUrl: './sidebar.component.html',
  styleUrl: './sidebar.component.css'
})

export class SidebarComponent {
  @Output() moduleSelected = new EventEmitter<string>();

  selectModule(name: string) {
    this.moduleSelected.emit(name);
  }
}

app.comp.css
 /* .layout {
      display: flex;
    }
    .content {
      flex: 1;
      padding: 20px;
      background: #f5f5f5;
    } */

    .layout {
  display: flex;
  height: 100vh;
}

.content {
  flex: 1;
  padding: 20px;
  background-color: #f4f4f4;
  overflow-y: auto;
}

.tab-bar {
  background: #ddd;
  padding: 8px 20px;
  display: flex;
  align-items: center;
  border-bottom: 1px solid #bbb;
}

.tab {
  background: white;
  padding: 5px 15px;
  border: 1px solid #ccc;
  border-radius: 8px;
  margin-right: 10px;
  display: flex;
  align-items: center;
  gap: 8px;
  font-weight: 500;
}

.tab i {
  cursor: pointer;
  color: #444;
}



.submodule-container {
  padding: 20px;
  border: 1px solid #ccc;
  margin-left: 250px; /* if sidebar is on the left */
}

.submodule-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #e9e9e9;
  padding: 10px;
  font-weight: bold;
}

.submodule-header button {
  border: none;
  background: transparent;
  font-size: 18px;
  cursor: pointer;
}

app.comp.html



<app-header
  [openedModule]="openedModule"
  (toggle)="handleToggle()"
  (closeModule)="closeModule()"
></app-header>

<div class="layout">
  <ng-container *ngIf="sidebarVisible">
    <!-- Show main sidebar only if no module is opened -->
    <app-sidebar
      *ngIf="!openedModule"
      (moduleSelected)="openModule($event)"
    ></app-sidebar>

    <!-- Show inventory sidebar -->
    <app-inventory-sidebar
      *ngIf="openedModule === 'Inventory Configuration'"
      (navigate)="navigateToSubModule($event)"
    ></app-inventory-sidebar>

    <!-- Add other sidebars for other modules here if needed -->
  </ng-container>

  <div class="content">
    <!-- Submodule components shown based on selectedSubModule -->
    <ng-container *ngIf="openedModule === 'Inventory Configuration'">
      <div *ngIf="selectedSubModule === 'manage-dashboard'">
        <app-manage-dashboard></app-manage-dashboard>
        <button (click)="closeSubModule()">Close</button>
      </div>

      <div *ngIf="selectedSubModule === 'recon-view-manager'">
        <app-recon-view-manager></app-recon-view-manager>
        <button (click)="closeSubModule()">Close</button>
      </div>

      <div *ngIf="selectedSubModule === 'model-categories'">
        <app-model-categories></app-model-categories>
        <button (click)="closeSubModule()">Close</button>
      </div>
    </ng-container>

    <!-- Default router outlet if no submodule is selected -->
    <router-outlet *ngIf="!selectedSubModule"></router-outlet>
  </div>
</div>

app.comp.ts

import { Component } from '@angular/core';
import { RouterModule, Router } from '@angular/router';
import { CommonModule } from '@angular/common';
import { HeaderComponent } from './header/header.component';
import { SidebarComponent } from './sidebar/sidebar.component';
import { InventorySidebarComponent } from './pages/inventory-configuration/inventory-sidebar/inventory-sidebar.component';
import { ManageDashboardComponent } from './pages/inventory-configuration/inventory-sidebar/manage-dashboard/manage-dashboard.component';
import { ReconViewManagerComponent } from './pages/inventory-configuration/inventory-sidebar/recon-view-manager/recon-view-manager.component';
import { ModelCategoriesComponent } from './pages/inventory-configuration/inventory-sidebar/model-categories/model-categories.component';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [
    CommonModule,
    RouterModule,
    HeaderComponent,
    SidebarComponent,
    InventorySidebarComponent,

     ManageDashboardComponent,
  ReconViewManagerComponent,
  ModelCategoriesComponent,
  ],
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css'],
})
export class AppComponent {
  sidebarVisible = false;
  openedModule: string | null = null;          // E.g. 'Inventory Configuration'
  selectedSubModule: string | null = null;      // E.g. 'manage-dashboard'

  constructor(private router: Router) {}

  // Toggle sidebar visibility
  handleToggle() {
    this.sidebarVisible = !this.sidebarVisible;
    if (!this.sidebarVisible) {
      this.openedModule = null;
      this.selectedSubModule = null;
      this.router.navigate(['']); // Default/blank route
    }
  }

  // Open main module
  openModule(moduleName: string) {
    this.openedModule = moduleName;
    this.selectedSubModule = null;
    this.sidebarVisible = true;

    if (moduleName === 'Inventory Configuration') {
      this.router.navigate(['/inventory-dashboard']); // Optional: default submodule
    }
  }

  // Close main module
  closeModule() {
    this.openedModule = null;
    this.selectedSubModule = null;
    this.router.navigate(['']);
  }

  // Open submodule within main module
  navigateToSubModule(subRoute: string) {
    this.selectedSubModule = subRoute;
    this.router.navigate([`/inventory/${subRoute}`]);
  }

  // Close only submodule
  closeSubModule() {
    this.selectedSubModule = null;
    this.router.navigate(['/inventory-dashboard']);
  }
}

app.routes.ts
import { Routes } from '@angular/router';
import { InventoryConfigurationComponent } from './pages/inventory-configuration/inventory-configuration.component';
import { SystemSetupComponent } from './pages/system-setup/system-setup.component';
import { AdminComponent } from './pages/admin/admin.component';
import { ImportExportManagerComponent } from './pages/import-export-manager/import-export-manager.component';
import { BlankComponent } from './pages/blank/blank.component';


import { ManageDashboardComponent } from './pages/inventory-configuration/inventory-sidebar/manage-dashboard/manage-dashboard.component';

import { ReconViewManagerComponent } from './pages/inventory-configuration/inventory-sidebar/recon-view-manager/recon-view-manager.component'; 
import { ModelCategoriesComponent } from './pages/inventory-configuration/inventory-sidebar/model-categories/model-categories.component';

export const routes: Routes = [
  { path: '', component: BlankComponent }, 
  { path: 'inventory', component: InventoryConfigurationComponent,
    children: [
       { path: 'manage-dashboard', component: ManageDashboardComponent },
      { path: 'recon-view-manager', component: ReconViewManagerComponent },
      { path: 'model-categories', component: ModelCategoriesComponent },
      { path: '', redirectTo: 'manage-dashboard', pathMatch: 'full' }
    ]
   },
  { path: 'system-setup', component: SystemSetupComponent },
  { path: 'admin', component: AdminComponent },
  { path: 'import-export', component: ImportExportManagerComponent }
];

styles.css
.main-container {
  display: flex;
}

app-sidebar {
  width: 250px;
}

.content {
  flex: 1;
  padding: 20px;
}




ng g c pages/inventory-configuration/inventory-sidebar/model-categories
ng g c pages/inventory-configuration/inventory-sidebar/recon-view-manager
 ng g c pages/inventory-configuration/inventory-sidebar/manage-dashboard  

 ng g c pages/inventory-configuration/inventory-sidebar
ng g c pages/blank                      

 npm install @fortawesome/fontawesome-free
 ng g c pages/import-export-manager       
ng g c pages/admin       
ng g c pages/system-setup                
 ng g c pages/inventory-configuration  
ng generate component sidebar        


index.html
<link
  rel="stylesheet"
  href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css"
  integrity="sha512-T4fQyP5IcGLlUjk5L2qD1x7g0Lrxy3aHc2PfD1s4M7rMZ5qIpH2XtqD3/fnMGpJxRP0kHfu3eHRcZG55gdP3cg=="
  crossorigin="anonymous"
  referrerpolicy="no-referrer"
/>

add this in angular.json
"styles": [
  "src/styles.css",
  "https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css"
]


________________________________________


Great! Here's the complete set of updated Angular code files you can copy-paste directly into your project to fully implement the "Manage Dashboard" feature.


---

✅ File 1: dashboard.service.ts

📁 src/app/pages/inventory-configuration/manage-dashboard/dashboard.service.ts

import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class DashboardService {
  private dashboards: any[] = [];

  getDashboards() {
    return this.dashboards;
  }

  addDashboard(dashboard: any) {
    this.dashboards.push(dashboard);
  }
}


import { Injectable } from '@angular/core';
import { Dashboard } from './dashboard.model';

@Injectable({
  providedIn: 'root'
})
export class DashboardService {
  private dashboards: Dashboard[] = [];

  getDashboards(): Dashboard[] {
    return this.dashboards;
  }

  addDashboard(dashboard: Dashboard): void {
    this.dashboards.push(dashboard);
  }
}


---

✅ File 2: manage-dashboard.component.ts

📁 src/app/pages/inventory-configuration/manage-dashboard/manage-dashboard.component.ts

import { Component } from '@angular/core';
import { DashboardService } from './dashboard.service';
import { BlankDashboardComponent } from './blank-dashboard.component';
import { InteractiveDashboardComponent } from './interactive-dashboard.component';

@Component({
  selector: 'app-manage-dashboard',
  standalone: true,
  imports: [BlankDashboardComponent, InteractiveDashboardComponent],
  templateUrl: './manage-dashboard.component.html',
})
export class ManageDashboardComponent {
  showManageDashboard = true;
  selectedDashboardType: string | null = null;
  dashboards = [];

  constructor(private dashboardService: DashboardService) {
    this.refreshDashboardList();
  }

  closeManageDashboard() {
    this.showManageDashboard = false;
  }

  selectDashboardType(type: string) {
    this.selectedDashboardType = type;
  }

  refreshDashboardList() {
    this.dashboards = this.dashboardService.getDashboards();
  }
}


---

✅ File 3: manage-dashboard.component.html

📁 src/app/pages/inventory-configuration/manage-dashboard/manage-dashboard.component.html

<div *ngIf="showManageDashboard">
  <h2>Manage Dashboard</h2>
  <button (click)="closeManageDashboard()">Close</button>

  <div>
    <button (click)="selectDashboardType('blank')">Blank Dashboard</button>
    <button (click)="selectDashboardType('interactive')">Interactive Dashboard</button>
  </div>

  <ng-container *ngIf="selectedDashboardType === 'blank'">
    <app-blank-dashboard (dashboardCreated)="refreshDashboardList()"></app-blank-dashboard>
  </ng-container>

  <ng-container *ngIf="selectedDashboardType === 'interactive'">
    <app-interactive-dashboard (dashboardCreated)="refreshDashboardList()"></app-interactive-dashboard>
  </ng-container>

  <table *ngIf="dashboards.length > 0">
    <tr>
      <th>Name</th><th>Description</th><th>Public</th><th>Created Date</th>
    </tr>
    <tr *ngFor="let d of dashboards">
      <td>{{ d.name }}</td>
      <td>{{ d.description }}</td>
      <td>{{ d.public ? 'Yes' : 'No' }}</td>
      <td>{{ d.createdDate }}</td>
    </tr>
  </table>

  <p *ngIf="dashboards.length === 0">No Rows To Show</p>
</div>


---


✅ File 6: interactive-dashboard.component.ts

📁 src/app/pages/inventory-configuration/manage-dashboard/interactive-dashboard.component.ts

import { Component, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-interactive-dashboard',
  standalone: true,
  template: `<p>Interactive dashboard coming soon.</p>`,
})
export class InteractiveDashboardComponent {
  @Output() dashboardCreated = new EventEmitter<void>();
}


---

✅ Update AppComponent (example)

📁 src/app/app.component.html

<button (click)="navigateToSubModule('manage-dashboard')">Manage Dashboard</button>

<app-manage-dashboard *ngIf="selectedSubModule === 'manage-dashboard'"></app-manage-dashboard>

📁 src/app/app.component.ts

Make sure you have something like:

export class AppComponent {
  selectedSubModule: string | null = null;

  navigateToSubModule(name: string) {
    this.selectedSubModule = name;
  }
}

___________________________________________________________________________________________________


blank-dashboard.component.ts

import { Component } from '@angular/core';
import { Component } from '@angular/core';
import { CommonModule } from '@angular/common';
import { FormsModule } from '@angular/forms';

@Component({
  selector: 'app-blank-dashboard',
  standalone: true,
  templateUrl: './blank-dashboard.component.html',
  styleUrls: ['./blank-dashboard.component.css'],
  imports: [CommonModule, FormsModule]  // ✅ Needed for ngIf, ngModel
})
export class BlankDashboardComponent {
  showModal = true;  // ✅ Show modal initially for testing
  isFullscreen = false;
  currentStep = 0;

  steps = ['Details', 'Content', 'Layout', 'Review'];

  formData = {
    name: '',
    description: '',
    visibility: 'Public'
  };

  toggleFullscreen() {
    this.isFullscreen = !this.isFullscreen;
  }

  closeModal() {
    this.showModal = false;
  }

  nextStep() {
    if (this.currentStep < this.steps.length - 1) {
      this.currentStep++;
    }
  }

  prevStep() {
    if (this.currentStep > 0) {
      this.currentStep--;
    }
  }

  submit() {
    console.log('Submitting form:', this.formData);
    this.closeModal(); // Auto close after submission
  }
}

✅ blank-dashboard.component.html
<!-- ✅ MODAL WRAPPED IN *ngIf="showModal" -->
<div *ngIf="showModal" class="modal-container" [class.fullscreen]="isFullscreen">
  <div class="modal-box">
    <div class="modal-header">
      <div class="header-left">
        <span class="material-symbols-outlined icon">dashboard</span>
        <h2>New Dashboard</h2>
      </div>
      <div class="header-actions">
        <button (click)="toggleFullscreen()" title="Fullscreen">🗖</button>
        <!-- ✅ CLOSE ICON CALLS closeModal() -->
        <button (click)="closeModal()" title="Close">✕</button>
      </div>
    </div>

    <div class="step-tracker">
      <div *ngFor="let step of steps; let i = index" class="step-item" [class.active]="i === currentStep">
        <div class="step-circle">{{ i + 1 }}</div>
        <span class="step-label">{{ step }}</span>
      </div>
    </div>

    <div class="modal-content">
      <!-- Step 1 -->
      <form *ngIf="currentStep === 0" #dashboardForm="ngForm" class="form-section">
        <div class="form-group">
          <label>Name <span class="required">*</span></label>
          <input type="text" [(ngModel)]="formData.name" name="name" placeholder="Add a name" required />
        </div>

        <div class="form-group">
          <label>Description</label>
          <textarea [(ngModel)]="formData.description" name="description" placeholder="Mention objective and purpose of dashboard"></textarea>
        </div>

        <div class="form-group">
          <label>Mark Dashboard As <span class="required">*</span></label>
          <div class="radio-options">
            <label>
              <input type="radio" [(ngModel)]="formData.visibility" name="visibility" value="Public" checked />
              <span class="custom-radio checked"></span> Public
            </label>
            <label>
              <input type="radio" [(ngModel)]="formData.visibility" name="visibility" value="Private" />
              <span class="custom-radio"></span> Private
            </label>
          </div>
          <small>Select <strong>Private</strong> to assign this dashboard to one or more users or teams.</small>
        </div>

        <div class="nav-buttons">
          <!-- ✅ CANCEL BUTTON CALLS closeModal() -->
          <button type="button" class="btn secondary" (click)="closeModal()">Cancel</button>
          <button type="button" class="btn primary" (click)="nextStep()">Next</button>
        </div>
      </form>

      <!-- Step 2 -->
      <div *ngIf="currentStep === 1">
        <p><strong>Step 2:</strong> Add your dashboard content here...</p>
        <div class="nav-buttons">
          <button class="btn secondary" (click)="prevStep()">Back</button>
          <button class="btn primary" (click)="nextStep()">Next</button>
        </div>
      </div>

      <!-- Step 3 -->
      <div *ngIf="currentStep === 2">
        <p><strong>Step 3:</strong> Choose your layout preferences...</p>
        <div class="nav-buttons">
          <button class="btn secondary" (click)="prevStep()">Back</button>
          <button class="btn primary" (click)="nextStep()">Next</button>
        </div>
      </div>

      <!-- Step 4 -->
      <div *ngIf="currentStep === 3">
        <p><strong>Step 4:</strong> Review and confirm your dashboard.</p>
        <div class="nav-buttons">
          <button class="btn secondary" (click)="prevStep()">Back</button>
          <button class="btn primary" (click)="submit()">Submit</button>
        </div>
      </div>
    </div>
  </div>
</div>

✅ blank-dashboard.component.css
.modal-container {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.modal-container.fullscreen .modal-box {
  width: 95vw;
  height: 95vh;
}

.modal-box {
  background: white;
  border-radius: 8px;
  box-shadow: 0 5px 30px rgba(0,0,0,0.3);
  max-width: 800px;
  width: 100%;
  padding: 20px;
  position: relative;
}

.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid #eee;
  padding-bottom: 10px;
}

.header-left {
  display: flex;
  align-items: center;
  gap: 8px;
}

.header-left .icon {
  font-size: 24px;
  color: #555;
}

.header-actions button {
  background: none;
  border: none;
  font-size: 18px;
  cursor: pointer;
  padding: 4px 8px;
}

.step-tracker {
  display: flex;
  gap: 25px;
  margin: 20px 0;
  align-items: center;
}

.step-item {
  display: flex;
  align-items: center;
  gap: 6px;
  color: gray;
}

.step-item.active {
  font-weight: bold;
  color: #0d9488;
}

.step-circle {
  width: 28px;
  height: 28px;
  border-radius: 50%;
  background-color: #ccc;
  display: flex;
  align-items: center;
  justify-content: center;
}

.step-item.active .step-circle {
  background-color: #0d9488;
  color: white;
}

.modal-content {
  margin-top: 10px;
}

.form-group {
  margin-bottom: 20px;
}

input[type="text"],
textarea {
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 6px;
}

textarea {
  height: 80px;
}

.radio-options {
  display: flex;
  gap: 20px;
  margin-top: 10px;
  align-items: center;
}

.radio-options input[type="radio"] {
  display: none;
}

.custom-radio {
  display: inline-block;
  width: 16px;
  height: 16px;
  border: 2px solid #aaa;
  border-radius: 50%;
  margin-right: 5px;
  vertical-align: middle;
}

.custom-radio.checked {
  border-color: #0d9488;
  background-color: #0d9488;
  position: relative;
}

.custom-radio.checked::after {
  content: '';
  display: block;
  width: 6px;
  height: 6px;
  margin: 3px auto;
  background: white;
  border-radius: 50%;
}

.required {
  color: red;
}

.nav-buttons {
  display: flex;
  justify-content: space-between;
  margin-top: 20px;
}

.btn {
  padding: 8px 16px;
  border-radius: 6px;
  cursor: pointer;
  border: none;
}

.btn.primary {
  background-color: #0d9488;
  color: white;
}

.btn.primary:hover {
  background-color: #0f766e;
}

.btn.secondary {
  background-color: #f3f4f6;
  color: #333;
  border: 1px solid #ccc;
}

.btn.secondary:hover {
  background-color: #e5e7eb;
}
___________________________________________________________________________________________________
manage-dashboard.comp.ts
import { Component, EventEmitter, Output } from '@angular/core';

@Component({
  selector: 'app-manage-dashboard',
  templateUrl: './manage-dashboard.component.html',
  styleUrls: ['./manage-dashboard.component.css']
})
export class ManageDashboardComponent {
  @Output() closeDashboard = new EventEmitter<void>();
  @Output() selectDashboard = new EventEmitter<string>();

  dashboards = [
    {
      id: 'blank',
      name: 'Blank Dashboard',
      icon: '📊',
      description: 'Start with a blank canvas'
    },
    {
      id: 'interactive',
      name: 'Interactive Dashboard',
      icon: '📈',
      description: 'Pre-built interactive components'
    }
  ];

  tableHeaders = ['Name', 'Description', 'Created By', 'Created Date', 'Modified By', 'Modified Date', 'Pu...', 'Acc...'];
  tableData: any[] = []; // Will be populated with data in the future

  onClose() {
    this.closeDashboard.emit();
  }

  onSelectDashboard(dashboardType: string) {
  if (dashboardType === 'blank') {
    this.showBlankDashboard = true;
    this.showInteractiveDashboard = false;
  } else if (dashboardType === 'interactive') {
    this.showInteractiveDashboard = true;
    this.showBlankDashboard = false;
  }
  this.selectDashboard.emit(dashboardType);
}

  onNewDashboard() {
    // Handle new dashboard creation
    console.log('New Dashboard clicked');
  }

  onBackToManage() {
  this.showBlankDashboard = false;
  this.showInteractiveDashboard = false;
 }
}


manage-dashboard.comp.html
<div class="manage-dashboard-container">
  <!-- Header -->
  <div class="header">
    <h2 class="title">Manage Dashboard</h2>
    <button class="close-btn" (click)="onClose()">×</button>
  </div>

  <!-- New Dashboard Button -->
  <div class="new-dashboard-section">
    <button class="new-dashboard-btn" (click)="onNewDashboard()">
      <span class="plus-icon">+</span>
      New Dashboard
    </button>
  </div>

  <!-- Dashboard Types -->
  <div class="dashboard-types">
    <div 
      class="dashboard-card" 
      *ngFor="let dashboard of dashboards"
      (click)="onSelectDashboard(dashboard.id)"
    >
      <div class="dashboard-icon">{{dashboard.icon}}</div>
      <div class="dashboard-name">{{dashboard.name}}</div>
    </div>
  </div>

  <!-- All Dashboards Section -->
  <div class="all-dashboards-section">
    <h3 class="section-title">All Dashboards</h3>
    
    <!-- Table -->
    <div class="table-container">
      <table class="dashboards-table">
        <thead>
          <tr>
            <th *ngFor="let header of tableHeaders">{{header}}</th>
          </tr>
        </thead>
        <tbody>
          <tr *ngIf="tableData.length === 0" class="no-data-row">
            <td [attr.colspan]="tableHeaders.length" class="no-data-cell">
              No Rows To Show
            </td>
          </tr>
          <!-- Future data rows will be rendered here -->
          <tr *ngFor="let row of tableData">
            <td *ngFor="let header of tableHeaders">
              {{row[header.toLowerCase().replace(' ', '')]}}
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</div>

manage.comp.css
.manage-dashboard-container {
  padding: 20px;
  background-color: #f5f5f5;
  min-height: 100vh;
  font-family: Arial, sans-serif;
}

/* Header */
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
  background-color: white;
  padding: 15px 20px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.title {
  margin: 0;
  font-size: 20px;
  font-weight: 600;
  color: #333;
}

.close-btn {
  background: none;
  border: none;
  font-size: 24px;
  cursor: pointer;
  color: #666;
  padding: 0;
  width: 30px;
  height: 30px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  transition: background-color 0.2s;
}

.close-btn:hover {
  background-color: #f0f0f0;
  color: #333;
}

/* New Dashboard Section */
.new-dashboard-section {
  margin-bottom: 30px;
}

.new-dashboard-btn {
  display: flex;
  align-items: center;
  gap: 8px;
  background-color: #007bff;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 6px;
  cursor: pointer;
  font-size: 14px;
  font-weight: 500;
  transition: background-color 0.2s;
}

.new-dashboard-btn:hover {
  background-color: #0056b3;
}

.plus-icon {
  font-size: 16px;
  font-weight: bold;
}

/* Dashboard Types */
.dashboard-types {
  display: flex;
  gap: 20px;
  margin-bottom: 40px;
}

.dashboard-card {
  background-color: white;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  padding: 30px 20px;
  text-align: center;
  cursor: pointer;
  transition: all 0.2s;
  min-width: 150px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.dashboard-card:hover {
  border-color: #007bff;
  box-shadow: 0 4px 8px rgba(0, 123, 255, 0.2);
  transform: translateY(-2px);
}

.dashboard-icon {
  font-size: 40px;
  margin-bottom: 15px;
}

.dashboard-name {
  font-size: 14px;
  font-weight: 500;
  color: #333;
}

/* All Dashboards Section */
.all-dashboards-section {
  background-color: white;
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.section-title {
  margin: 0 0 20px 0;
  font-size: 16px;
  font-weight: 600;
  color: #333;
}

/* Table */
.table-container {
  overflow-x: auto;
}

.dashboards-table {
  width: 100%;
  border-collapse: collapse;
  background-color: white;
}

.dashboards-table th {
  background-color: #f8f9fa;
  padding: 12px 16px;
  text-align: left;
  font-weight: 600;
  color: #555;
  border-bottom: 2px solid #e9ecef;
  font-size: 13px;
}

.dashboards-table td {
  padding: 12px 16px;
  border-bottom: 1px solid #e9ecef;
  color: #333;
  font-size: 13px;
}

.dashboards-table tbody tr:hover {
  background-color: #f8f9fa;
}

.no-data-row {
  background-color: transparent !important;
}

.no-data-cell {
  text-align: center;
  color: #666;
  font-style: italic;
  padding: 40px 16px !important;
}

/* Responsive */
@media (max-width: 768px) {
  .manage-dashboard-container {
    padding: 15px;
  }
  
  .dashboard-types {
    flex-direction: column;
    gap: 15px;
  }
  
  .dashboard-card {
    min-width: auto;
  }
  
  .header {
    padding: 12px 15px;
  }
  
  .title {
    font-size: 18px;
  }
}
______________________________________________________________________________________________________________________________________________________________
manage-dashboard.component.ts
import { Component, EventEmitter, Output } from '@angular/core';
import { CommonModule } from '@angular/common';

@Component({
  selector: 'app-manage-dashboard',
  templateUrl: './manage-dashboard.component.html',
  styleUrls: ['./manage-dashboard.component.css']
})
export class ManageDashboardComponent {
  @Output() closeDashboard = new EventEmitter<void>();
  @Output() selectDashboard = new EventEmitter<string>();

  showBlankDashboard = false;
  showInteractiveDashboard = false;

  dashboards = [
    {
      id: 'blank',
      name: 'Blank Dashboard',
      icon: '📊',
      description: 'Start with a blank canvas'
    },
    {
      id: 'interactive',
      name: 'Interactive Dashboard',
      icon: '📈',
      description: 'Pre-built interactive components'
    }
  ];

  tableHeaders = ['Name', 'Description', 'Created By', 'Created Date', 'Modified By', 'Modified Date', 'Pu...', 'Acc...'];
  tableData: any[] = []; // Will be populated with data in the future

  onClose() {
    this.closeDashboard.emit();
  }

  onSelectDashboard(dashboardType: string) {
    this.selectDashboard.emit(dashboardType);
  }

  onNewDashboard() {
    // Handle new dashboard creation
    console.log('New Dashboard clicked');
  }
}


manage-dashboard.component.html
<div class="manage-dashboard-container">
  <!-- Main Manage Dashboard View -->
  <div *ngIf="!showBlankDashboard && !showInteractiveDashboard">
    <!-- Header -->
    <div class="header">
      <h2 class="title">Manage Dashboard</h2>
      <button class="close-btn" (click)="onClose()">×</button>
    </div>

    <!-- New Dashboard Button -->
    <div class="new-dashboard-section">
      <button class="new-dashboard-btn" (click)="onNewDashboard()">
        <span class="plus-icon">+</span>
        New Dashboard
      </button>
    </div>

    <!-- Dashboard Types -->
    <div class="dashboard-types">
      <div 
        class="dashboard-card" 
        *ngFor="let dashboard of dashboards"
        (click)="onSelectDashboard(dashboard.id)"
      >
        <div class="dashboard-icon">{{dashboard.icon}}</div>
        <div class="dashboard-name">{{dashboard.name}}</div>
      </div>
    </div>

    <!-- All Dashboards Section -->
    <div class="all-dashboards-section">
      <h3 class="section-title">All Dashboards</h3>
      
      <!-- Table -->
      <div class="table-container">
        <table class="dashboards-table">
          <thead>
            <tr>
              <th *ngFor="let header of tableHeaders">{{header}}</th>
            </tr>
          </thead>
          <tbody>
            <tr *ngIf="tableData.length === 0" class="no-data-row">
              <td [attr.colspan]="tableHeaders.length" class="no-data-cell">
                No Rows To Show
              </td>
            </tr>
            <!-- Future data rows will be rendered here -->
            <tr *ngFor="let row of tableData">
              <td *ngFor="let header of tableHeaders">
                {{row[header.toLowerCase().replace(' ', '')]}}
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>

  <!-- Blank Dashboard View -->
  <div *ngIf="showBlankDashboard">
    <app-blank-dashboard></app-blank-dashboard>
  </div>

  <!-- Interactive Dashboard View -->
  <div *ngIf="showInteractiveDashboard" class="dashboard-view">
    <div class="dashboard-header">
      <button class="back-btn" (click)="onBackToManage()">← Back to Manage</button>
      <button class="close-btn" (click)="onClose()">×</button>
    </div>
    <!-- Add your interactive dashboard component here -->
    <!-- <app-interactive-dashboard></app-interactive-dashboard> -->
    <div class="placeholder">Interactive Dashboard Component will be rendered here</div>
  </div>
</div>


app.comp.css
.layout {
  display: flex;
  justify-content: space-between;
}

.layout .content {
  flex-grow: 1;
  margin-left: 16px; /* Optional: Add spacing between sidebar and content */
}

.layout app-sidebar, .layout app-inventory-sidebar {
  width: 250px; /* Sidebar width */
  flex-shrink: 0;
}

.layout .content {
  padding: 20px;
  overflow-y: auto; /* To avoid overflow issues */
}
&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&

✅ Updated blank-dashboard.component.ts
import { Component } from '@angular/core';
import { CommonModule } from '@angular/common';
import { FormsModule } from '@angular/forms';

@Component({
  selector: 'app-blank-dashboard',
  standalone: true,
  templateUrl: './blank-dashboard.component.html',
  styleUrls: ['./blank-dashboard.component.css'],
  imports: [CommonModule, FormsModule]
})
export class BlankDashboardComponent {
  showModal = true;
  isFullscreen = false;
  currentStep = 0;

  steps = ['Details', 'Content', 'Layout', 'Review'];

  formData = {
    name: '',
    description: '',
    visibility: 'Public'
  };

  selectedChart = 'bar';  // Default selected chart type

  toggleFullscreen() {
    this.isFullscreen = !this.isFullscreen;
  }

  closeModal() {
    this.showModal = false;
  }

  nextStep() {
    if (this.currentStep < this.steps.length - 1) {
      this.currentStep++;
    }
  }

  prevStep() {
    if (this.currentStep > 0) {
      this.currentStep--;
    }
  }

  submit() {
    console.log('Submitting form:', this.formData);
    this.closeModal();
  }

  setChartType(type: string) {
    this.selectedChart = type;
  }
}
✅ Updated HTML (Only the Step 2 section of blank-dashboard.component.html)
<!-- Step 2 -->
<div *ngIf="currentStep === 1" class="content-step">
  <div class="sidebar">
    <h4>Select Card</h4>
    <ul>
      <li [class.active]="selectedChart === 'bar'" (click)="setChartType('bar')">A. Case Queue by Data Element (Bar Chart)</li>
      <li [class.active]="selectedChart === 'pie'" (click)="setChartType('pie')">B. Case Queue by Data Element (Pie Chart)</li>
    </ul>
  </div>
  <div class="chart-preview">
    <ng-container [ngSwitch]="selectedChart">
      <div *ngSwitchCase="'bar'">
        <h3>Bar Chart Preview</h3>
        <!-- Simulated chart block -->
        <div class="chart-bar">[Bar Chart Placeholder]</div>
      </div>
      <div *ngSwitchCase="'pie'">
        <h3>Pie Chart Preview</h3>
        <!-- Simulated chart block -->
        <div class="chart-pie">[Pie Chart Placeholder]</div>
      </div>
    </ng-container>
    <div class="nav-buttons">
      <button class="btn secondary" (click)="prevStep()">Back</button>
      <button class="btn primary" (click)="nextStep()">Next</button>
    </div>
  </div>
</div>

css
.content-step {
  display: flex;
  gap: 20px;
}

.sidebar {
  width: 250px;
  background: #f9fafb;
  padding: 15px;
  border-right: 1px solid #ddd;
}

.sidebar h4 {
  margin-bottom: 10px;
}

.sidebar ul {
  list-style: none;
  padding: 0;
}

.sidebar li {
  padding: 8px;
  cursor: pointer;
  border-radius: 4px;
  margin-bottom: 6px;
}

.sidebar li:hover,
.sidebar li.active {
  background-color: #0d9488;
  color: white;
}

.chart-preview {
  flex: 1;
  padding: 15px;
  background: #ffffff;
  border: 1px solid #e5e7eb;
  border-radius: 6px;
}

.chart-bar,
.chart-pie {
  height: 200px;
  background: #e0f2f1;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
  color: #0d9488;
  margin-top: 10px;
  border-radius: 4px;
}


<!-- Step 2 -->
<div *ngIf="currentStep === 1" class="content-step">
  <div class="sidebar">
    <h4>Select Card</h4>
    <ul>
      <li [class.active]="selectedChart === 'bar'" (click)="setChartType('bar')">
        A. Case Queue by Data Element (Bar Chart)
      </li>
      <li [class.active]="selectedChart === 'pie'" (click)="setChartType('pie')">
        B. Case Queue by Data Element (Pie Chart)
      </li>
    </ul>
  </div>

  <div class="chart-preview">
    <ng-container [ngSwitch]="selectedChart">
      <div *ngSwitchCase="'bar'">
        <img src="assets/images/bar-chart-preview.png" alt="Bar Chart" style="width: 100%; max-width: 300px;" />
      </div>
      <div *ngSwitchCase="'pie'">
        <img src="assets/images/pie-chart-preview.png" alt="Pie Chart" style="width: 100%; max-width: 300px;" />
      </div>
    </ng-container>

    <div class="form-section">
      <h4>Configure Card: Case Queue by Data Element of type {{ selectedChart === 'bar' ? 'Bar Chart' : 'Pie Chart' }}</h4>

      <label>Description</label>
      <p>Case Queue by Data Element of type {{ selectedChart === 'bar' ? 'Bar Chart' : 'Pie Chart' }}</p>

      <label>Title *</label>
      <input type="text" [(ngModel)]="title" [value]="'Case Queue by Data Element of type ' + (selectedChart === 'bar' ? 'Bar Chart' : 'Pie Chart')" />

      <label>Model *</label>
      <select [(ngModel)]="model">
        <option *ngFor="let option of modelOptions" [value]="option">{{ option }}</option>
      </select>

      <label>Group By *</label>
      <select [(ngModel)]="groupBy">
        <option *ngFor="let group of groupByOptions" [value]="group">{{ group }}</option>
      </select>

      <label>Aggregation</label>
      <p>Aggregation Type</p>

      <label>Aggregation Field</label>
      <select [(ngModel)]="aggregationField">
        <option *ngFor="let field of aggregationFields" [value]="field">{{ field }}</option>
      </select>

      <button class="btn add-btn" (click)="addCard()">Add</button>
    </div>

    <div class="nav-buttons">
      <button class="btn secondary" (click)="prevStep()">Back</button>
      <button class="btn primary" (click)="nextStep()">Next</button>
    </div>
  </div>
</div>

ts
selectedChart = 'bar';
title = '';
model = '';
groupBy = '';
aggregationField = '';

modelOptions = ['Germany_Holdings', 'Luxembourg_Holdings', 'Monacco_Holdings'];
groupByOptions = ['Amount', 'Case Id', 'Create Date', 'Custom Value'];
aggregationFields = ['count', 'sum'];

setChartType(type: string): void {
  this.selectedChart = type;
  this.title = `Case Queue by Data Element of type ${type === 'bar' ? 'Bar Chart' : 'Pie Chart'}`;
}

addCard(): void {
  // Validation logic and storing form values
  console.log('Card added:', {
    chartType: this.selectedChart,
    title: this.title,
    model: this.model,
    groupBy: this.groupBy,
    aggregationField: this.aggregationField
  });
}

css
.chart-image {
  max-width: 100%;
  height: auto;
  margin-bottom: 20px;
  border: 1px solid #ccc;
  border-radius: 6px;
}

.chart-details {
  margin-top: 20px;
  background: #f9fafb;
  padding: 20px;
  border-radius: 8px;
  border: 1px solid #eee;
}

.form-group {
  margin-bottom: 15px;
}

input, select {
  width: 100%;
  padding: 8px;
  margin-top: 5px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.add-btn {
  background-color: #4caf50;
  color: white;
  margin-top: 10px;
}
------------------------------------------------------------------------------------------------------------------------
✅ Updated HTML for Initial and Content Pages:
<!-- Step 1 -->
<form *ngIf="currentStep === 0" #dashboardForm="ngForm" class="form-section">
  <div class="form-group">
    <label>Name <span class="required">*</span></label>
    <input type="text" [(ngModel)]="formData.name" name="name" placeholder="Add a name" required />
  </div>

  <div class="form-group">
    <label>Description</label>
    <textarea [(ngModel)]="formData.description" name="description" placeholder="Mention description..."></textarea>
  </div>

  <div class="form-group">
    <label>Mark Dashboard As <span class="required">*</span></label>
    <div class="radio-options">
      <label>
        <input type="radio" [(ngModel)]="formData.visibility" name="visibility" value="Public" />
        <span class="custom-radio"></span> Public
      </label>
      <label>
        <input type="radio" [(ngModel)]="formData.visibility" name="visibility" value="Private" />
        <span class="custom-radio"></span> Private
      </label>
    </div>
    <small>Select <strong>Private</strong> to assign this dashboard to one or more users or teams.</small>
  </div>

  <div class="nav-buttons">
    <button type="button" class="btn secondary" (click)="closeModal()">Cancel</button>
    <button type="button" class="btn primary" (click)="nextStep()">Next</button>
  </div>
</form>

<!-- Step 2 -->
<div *ngIf="currentStep === 1" class="content-step" style="display: flex;">
  <div class="sidebar" style="flex: 1; padding: 1rem;">
    <h4>Select Card</h4>
    <ul>
      <li [class.active]="selectedChart === 'bar'" (click)="setChartType('bar')">Case Queue by Data Element (Bar Chart)</li>
      <li [class.active]="selectedChart === 'pie'" (click)="setChartType('pie')">Case Queue by Data Element (Pie Chart)</li>
    </ul>
  </div>

  <div class="chart-preview" style="flex: 2; padding: 1rem;">
    <ng-container [ngSwitch]="selectedChart">
      <div *ngSwitchCase="'bar'">
        <h3>Bar Chart Preview</h3>
        <div class="chart-bar">[Bar Chart Placeholder]</div>
      </div>
      <div *ngSwitchCase="'pie'">
        <h3>Pie Chart Preview</h3>
        <div class="chart-pie">[Pie Chart Placeholder]</div>
      </div>
    </ng-container>

    <div class="form-section" style="max-height: 300px; overflow-y: auto; margin-top: 1rem;">
      <h4>Configure Card: Case Queue by Data Element of type {{ selectedChart === 'bar' ? 'Bar Chart' : 'Pie Chart' }}</h4>

      <label>Title <span class="required">*</span></label>
      <input type="text" [(ngModel)]="title" name="title" required />

      <label>Model <span class="required">*</span></label>
      <select [(ngModel)]="model" name="model" required>
        <option *ngFor="let option of modelOptions" [value]="option">{{ option }}</option>
      </select>

      <label>Group By <span class="required">*</span></label>
      <select [(ngModel)]="groupBy" name="groupBy" required>
        <option *ngFor="let group of groupByOptions" [value]="group">{{ group }}</option>
      </select>

      <label>Aggregation</label>
      <select [(ngModel)]="aggregation" name="aggregation">
        <option *ngFor="let agg of aggregationTypes" [value]="agg">{{ agg }}</option>
      </select>

      <label>Aggregation Field</label>
      <select [(ngModel)]="aggregationField" name="aggregationField">
        <option *ngFor="let field of aggregationFields" [value]="field">{{ field }}</option>
      </select>

      <button class="btn add-btn" style="margin-top: 10px;" (click)="addCard()">Add</button>
    </div>

    <div class="nav-buttons" style="margin-top: 20px;">
      <button class="btn secondary" (click)="prevStep()">Back to Initial</button>
      <button class="btn primary" (click)="nextStep()">Next to Layout</button>
    </div>
  </div>
</div>

✅ Updated TypeScript Changes:
Update your BlankDashboardComponent class with these fixes:
export class BlankDashboardComponent {
  showModal = true;
  isFullscreen = false;
  currentStep = 0;

  steps = ['Initial', 'Content', 'Layout', 'Review'];

  formData = {
    name: '',
    description: '',
    visibility: 'Public'
  };

  selectedChart = 'bar';
  title = '';
  model = '';
  groupBy = '';
  aggregation = '';
  aggregationField = '';

  modelOptions = ['Germany_Holdings', 'Luxembourg_Holdings', 'Monacco_Holdings'];
  groupByOptions = ['Amount', 'Case Id', 'Create Date', 'Custom Value'];
  aggregationTypes = ['Count', 'Sum', 'Average', 'Max', 'Min']; // Dummy values
  aggregationFields = ['Total Amount', 'Case Number', 'Score']; // Dummy values

  toggleFullscreen() {
    this.isFullscreen = !this.isFullscreen;
  }

  closeModal() {
    this.showModal = false;
    this.dashboardClose?.emit();
  }

  nextStep() {
    if (this.currentStep === 0 && !this.formData.name.trim()) {
      alert('Please fill in the required "Name" field.');
      return;
    }
    if (this.currentStep < this.steps.length - 1) {
      this.currentStep++;
    }
  }

  prevStep() {
    if (this.currentStep > 0) {
      this.currentStep--;
    }
  }

  submit() {
    alert('Dashboard submitted successfully!');
    console.log('Submitted Data:', this.formData);
  }

  setChartType(type: string): void {
    this.selectedChart = type;
    this.title = `Case Queue by Data Element of type ${type === 'bar' ? 'Bar Chart' : 'Pie Chart'}`;
  }

  addCard(): void {
    // You may add validation here
    console.log('Card added:', {
      chartType: this.selectedChart,
      title: this.title,
      model: this.model,
      groupBy: this.groupBy,
      aggregation: this.aggregation,
      aggregationField: this.aggregationField
    });
  }
}


/* Generic Modal Styles */
.modal-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0,0,0,0.6);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.modal-box {
  background: #fff;
  width: 90%;
  max-width: 1000px;
  max-height: 90vh;
  overflow: auto;
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0 8px 16px rgba(0,0,0,0.2);
}

.fullscreen .modal-box {
  width: 100%;
  height: 100%;
  border-radius: 0;
}

/* Header */
.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.header-left {
  display: flex;
  align-items: center;
  gap: 10px;
}

.header-actions button {
  background: none;
  border: none;
  font-size: 20px;
  cursor: pointer;
}

/* Step Tracker */
.step-tracker {
  display: flex;
  justify-content: space-between;
  margin: 20px 0;
}

.step-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  flex: 1;
  position: relative;
}

.step-circle {
  width: 30px;
  height: 30px;
  background: #ccc;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.step-item.active .step-circle {
  background-color: #007bff;
  color: #fff;
}

.step-label {
  margin-top: 5px;
  font-size: 12px;
}

/* Form Section */
.form-section {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.form-group {
  display: flex;
  flex-direction: column;
}

.required {
  color: red;
}

/* Radio Buttons */
.radio-options {
  display: flex;
  gap: 20px;
}

.radio-options label {
  display: flex;
  align-items: center;
  gap: 5px;
}

/* Buttons */
.nav-buttons {
  display: flex;
  justify-content: flex-end;
  gap: 10px;
  margin-top: 20px;
}

.btn {
  padding: 8px 14px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.btn.primary {
  background-color: #007bff;
  color: white;
}

.btn.secondary {
  background-color: #ccc;
  color: black;
}

.btn.add-btn {
  background-color: green;
  color: white;
}

/* Step 2 - Content */
.content-step {
  display: flex;
  gap: 20px;
  margin-top: 20px;
}

.sidebar {
  width: 30%;
  background: #f8f8f8;
  padding: 10px;
  border-right: 1px solid #ddd;
}

.sidebar ul {
  list-style-type: none;
  padding-left: 0;
}

.sidebar li {
  padding: 10px;
  cursor: pointer;
  border-radius: 4px;
}

.sidebar li.active {
  background-color: #007bff;
  color: white;
}

.chart-preview {
  width: 70%;
  overflow-y: auto;
  max-height: 400px;
}

.chart-bar,
.chart-pie {
  background-color: #e0e0e0;
  height: 200px;
  margin-bottom: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Inputs and selects */
input[type="text"],
textarea,
select {
  width: 100%;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

/* Responsive Fix */
@media (max-width: 768px) {
  .content-step {
    flex-direction: column;
  }

  .sidebar,
  .chart-preview {
    width: 100%;
  }

  .chart-preview {
    max-height: unset;
  }
}


___________________________________________________________________________________


deleteDashboard(dashboard: any) {
  if (confirm(`Are you sure you want to delete "${dashboard.name}"?`)) {
    this.dashboardService.deleteDashboard(dashboard.id).subscribe({
      next: () => {
        alert('Dashboard deleted successfully');
        this.loadDashboards(); // refresh list
      },
      error: err => {
        console.error('Delete failed:', err);
        alert('Failed to delete dashboard');
      }
    });
  }
}



@Input() editData: any;

ngOnInit() {
  if (this.editData) {
    this.formData.name = this.editData.name;
    this.formData.description = this.editData.description;
    this.formData.visibility = this.editData.public ? 'Public' : 'Private';

    // optional fields
    this.model = this.editData.model;
    this.groupBy = this.editData.groupBy;
    this.aggregation = this.editData.aggregation;
    this.aggregationField = this.editData.aggregationField;
  }
}



submit() {
  const dashboard = {
    id: this.editData?.id,
    name: this.formData.name,
    description: this.formData.description,
    createdBy: 'admin',
    createdDate: this.editData?.createdDate || new Date().toISOString(),
    modifiedBy: 'admin',
    modifiedDate: new Date().toISOString(),
    isPublic: this.formData.visibility === 'Public',
    model: this.model,
    groupBy: this.groupBy,
    aggregation: this.aggregation,
    aggregationField: this.aggregationField
  };

  const request = dashboard.id
    ? this.dashboardService.updateDashboard(dashboard)
    : this.dashboardService.addDashboard(dashboard);

  request.subscribe({
    next: () => {
      alert('Dashboard saved successfully!');
      this.router.navigate(['/inventory/manage-dashboard']);
    },
    error: err => {
      console.error('Failed to save dashboard:', err);
      alert('Failed to save dashboard');
    }
  });
}
