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

✅ File 4: blank-dashboard.component.ts

📁 src/app/pages/inventory-configuration/manage-dashboard/blank-dashboard.component.ts

import { Component, Output, EventEmitter } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { DashboardService } from './dashboard.service';

@Component({
  selector: 'app-blank-dashboard',
  standalone: true,
  imports: [FormsModule],
  templateUrl: './blank-dashboard.component.html',
})
export class BlankDashboardComponent {
  currentStep = 1;
  dashboard = {
    name: '',
    description: '',
    public: true
  };

  @Output() dashboardCreated = new EventEmitter<void>();

  constructor(private dashboardService: DashboardService) {}

  nextStep() {
    if (this.currentStep < 4) {
      this.currentStep++;
    } else {
      this.saveDashboard();
    }
  }

  saveDashboard() {
    const newDashboard = {
      ...this.dashboard,
      createdBy: 'User1',
      createdDate: new Date().toISOString(),
    };
    this.dashboardService.addDashboard(newDashboard);
    this.dashboardCreated.emit();
    this.currentStep = 1;
    this.dashboard = { name: '', description: '', public: true };
  }
}



import { Component, Output, EventEmitter } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { DashboardService } from './dashboard.service';
import { Dashboard } from './dashboard.model';

@Component({
  selector: 'app-blank-dashboard',
  standalone: true,
  imports: [FormsModule],
  templateUrl: './blank-dashboard.component.html',
})
export class BlankDashboardComponent {
  currentStep = 1;

  dashboard: Omit<Dashboard, 'createdBy' | 'createdDate'> = {
    name: '',
    description: '',
    public: true
  };

  @Output() dashboardCreated = new EventEmitter<void>();

  constructor(private dashboardService: DashboardService) {}

  nextStep() {
    if (this.currentStep < 4) {
      this.currentStep++;
    } else {
      this.saveDashboard();
    }
  }

  saveDashboard() {
    const newDashboard: Dashboard = {
      ...this.dashboard,
      createdBy: 'User1',
      createdDate: new Date().toISOString(),
    };
    this.dashboardService.addDashboard(newDashboard);
    this.dashboardCreated.emit();
    this.currentStep = 1;
    this.dashboard = { name: '', description: '', public: true };
  }
}

---

✅ File 5: blank-dashboard.component.html

📁 src/app/pages/inventory-configuration/manage-dashboard/blank-dashboard.component.html

<div *ngIf="currentStep === 1">
  <h3>Step 1: Basic Info</h3>
  <input placeholder="Dashboard Name" [(ngModel)]="dashboard.name" />
  <input placeholder="Description" [(ngModel)]="dashboard.description" />
  <label>
    <input type="radio" [(ngModel)]="dashboard.public" [value]="true" /> Public
  </label>
  <label>
    <input type="radio" [(ngModel)]="dashboard.public" [value]="false" /> Private
  </label>
  <button (click)="nextStep()">Next</button>
</div>

<div *ngIf="currentStep === 2">
  <h3>Step 2: Content</h3>
  <!-- Add form fields for content later -->
  <button (click)="nextStep()">Next</button>
</div>

<div *ngIf="currentStep === 3">
  <h3>Step 3: Layout</h3>
  <!-- Add layout options later -->
  <button (click)="nextStep()">Next</button>
</div>

<div *ngIf="currentStep === 4">
  <h3>Step 4: Review</h3>
  <p><strong>Name:</strong> {{dashboard.name}}</p>
  <p><strong>Description:</strong> {{dashboard.description}}</p>
  <p><strong>Visibility:</strong> {{dashboard.public ? 'Public' : 'Private'}}</p>
  <button (click)="nextStep()">Create</button>
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


--------------------------------------------------------------------------------------------
blank-dashboard.component.html

<div class="modal" [class.fullscreen]="isFullscreen">
  <div class="modal-header">
    <h2>New Dashboard</h2>
    <div class="modal-actions">
      <button (click)="toggleFullscreen()">🗖</button>
      <button (click)="closeModal()">✕</button>
    </div>
  </div>

  <div class="step-indicator">
    <div *ngFor="let step of steps; let i = index"
         [class.active]="i === currentStep"
         class="step">
      {{ i + 1 }} {{ step }}
    </div>
  </div>

  <div class="modal-content">
    <!-- Step 1 -->
    <form *ngIf="currentStep === 0" #dashboardForm="ngForm">
      <label for="name">Name<span class="required">*</span></label>
      <input type="text" id="name" name="name" [(ngModel)]="formData.name" required placeholder="Add a name">

      <label for="description">Description</label>
      <input type="text" id="description" name="description" [(ngModel)]="formData.description" placeholder="Mention objective and purpose of dashboard">

      <label>Mark Dashboard As</label>
      <div class="radio-group">
        <label><input type="radio" name="visibility" value="Public" [(ngModel)]="formData.visibility" checked> Public</label>
        <label><input type="radio" name="visibility" value="Private" [(ngModel)]="formData.visibility"> Private</label>
      </div>
      <small>Select <strong>Private</strong> to assign this dashboard to one or more users or teams.</small>

      <div class="navigation-buttons">
        <button type="button" (click)="nextStep()">Next</button>
      </div>
    </form>

    <!-- Step 2 -->
    <div *ngIf="currentStep === 1">
      <p><strong>Step 2:</strong> Add your dashboard content here...</p>
      <div class="navigation-buttons">
        <button (click)="prevStep()">Back</button>
        <button (click)="nextStep()">Next</button>
      </div>
    </div>

    <!-- Step 3 -->
    <div *ngIf="currentStep === 2">
      <p><strong>Step 3:</strong> Choose your layout preferences...</p>
      <div class="navigation-buttons">
        <button (click)="prevStep()">Back</button>
        <button (click)="nextStep()">Next</button>
      </div>
    </div>

    <!-- Step 4 -->
    <div *ngIf="currentStep === 3">
      <p><strong>Step 4:</strong> Review and confirm your dashboard.</p>
      <div class="navigation-buttons">
        <button (click)="prevStep()">Back</button>
        <button (click)="submit()">Submit</button>
      </div>
    </div>
  </div>
</div>


---

🎨 blank-dashboard.component.css

.modal {
  width: 600px;
  margin: 30px auto;
  border: 1px solid #ccc;
  background: #fff;
  border-radius: 6px;
  box-shadow: 0 5px 15px rgba(0,0,0,0.3);
  overflow: hidden;
  padding: 20px;
}

.modal.fullscreen {
  width: 95vw;
  height: 95vh;
  position: fixed;
  top: 2.5vh;
  left: 2.5vw;
  z-index: 1000;
}

.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.modal-actions button {
  margin-left: 5px;
  cursor: pointer;
}

.step-indicator {
  display: flex;
  justify-content: space-between;
  margin: 15px 0;
}

.step {
  flex: 1;
  text-align: center;
  padding: 5px;
  background: #eee;
  border-radius: 4px;
}

.step.active {
  background-color: #2196f3;
  color: #fff;
  font-weight: bold;
}

.modal-content {
  margin-top: 15px;
}

input[type="text"] {
  width: 100%;
  margin: 5px 0 10px;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.radio-group {
  display: flex;
  gap: 20px;
  margin: 10px 0;
}

.required {
  color: red;
}

.navigation-buttons {
  margin-top: 15px;
  display: flex;
  justify-content: space-between;
}


---

⚙️ blank-dashboard.component.ts

import { Component } from '@angular/core';

@Component({
  selector: 'app-blank-dashboard',
  templateUrl: './blank-dashboard.component.html',
  styleUrls: ['./blank-dashboard.component.css']
})
export class BlankDashboardComponent {
  isFullscreen = false;
  currentStep = 0;

  steps = ['Initial', 'Content', 'Layout', 'Review'];

  formData = {
    name: '',
    description: '',
    visibility: 'Public'
  };

  toggleFullscreen() {
    this.isFullscreen = !this.isFullscreen;
  }

  closeModal() {
    // You can add logic to hide or destroy the component/modal
    alert('Modal closed!');
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
    // You can also emit this data or call an API
  }
}
______________________________________________________________________________________________________________________________________________________________________________________________________


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
