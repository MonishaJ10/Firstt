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

To implement the described dashboard feature in Angular, here's a step-by-step breakdown:


---

🧩 1. Project Structure Example

src/
├── app/
│   ├── components/
│   │   ├── manage-dashboard/
│   │   │   ├── manage-dashboard.component.ts/html/css
│   │   │   ├── blank-dashboard.component.ts/html/css
│   │   │   ├── interactive-dashboard.component.ts/html/css
│   │   │   ├── dashboard-steps/
│   │   │   │   ├── initial-step.component.ts
│   │   │   │   ├── content-step.component.ts
│   │   │   │   ├── layout-step.component.ts
│   │   │   │   ├── review-step.component.ts
│   ├── services/
│   │   ├── dashboard.service.ts


---

📌 2. Manage Dashboard Component

manage-dashboard.component.html

<div *ngIf="showManageDashboard" class="dashboard-container">
  <div class="dashboard-header">
    <span>Manage Dashboard</span>
    <button (click)="closeManageDashboard()">X</button>
  </div>

  <div class="new-dashboard">
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
    <thead>
      <tr>
        <th>Name</th><th>Description</th><th>Created By</th><th>Created Date</th>
        <th>Modified By</th><th>Modified Date</th><th>Public</th>
      </tr>
    </thead>
    <tbody>
      <tr *ngFor="let d of dashboards">
        <td>{{ d.name }}</td>
        <td>{{ d.description }}</td>
        <td>{{ d.createdBy }}</td>
        <td>{{ d.createdDate }}</td>
        <td>{{ d.modifiedBy }}</td>
        <td>{{ d.modifiedDate }}</td>
        <td>{{ d.public ? 'Yes' : 'No' }}</td>
      </tr>
    </tbody>
  </table>

  <p *ngIf="dashboards.length === 0">No Rows To Show</p>
</div>

manage-dashboard.component.ts

export class ManageDashboardComponent {
  showManageDashboard = true;
  selectedDashboardType: string | null = null;
  dashboards = [];

  constructor(private dashboardService: DashboardService) {}

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

🧱 3. Blank Dashboard with Step Flow

blank-dashboard.component.ts

export class BlankDashboardComponent {
  currentStep = 1;
  dashboard = {
    name: '',
    description: '',
    public: true
  };

  @Output() dashboardCreated = new EventEmitter<void>();

  nextStep() {
    if (this.currentStep < 4) {
      this.currentStep++;
    } else {
      // Final Step - Save dashboard
      this.saveDashboard();
    }
  }

  saveDashboard() {
    const newDashboard = {
      ...this.dashboard,
      createdBy: 'User1',
      createdDate: new Date().toISOString(),
      modifiedBy: '',
      modifiedDate: '',
    };
    this.dashboardService.addDashboard(newDashboard);
    this.dashboardCreated.emit();
  }
}

blank-dashboard.component.html

<div *ngIf="currentStep === 1">
  <h3>Initial</h3>
  <input placeholder="Add a name" [(ngModel)]="dashboard.name" required />
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
  <h3>Content</h3>
  <button (click)="nextStep()">Next</button>
</div>

<div *ngIf="currentStep === 3">
  <h3>Layout</h3>
  <button (click)="nextStep()">Next</button>
</div>

<div *ngIf="currentStep === 4">
  <h3>Review</h3>
  <p><strong>Name:</strong> {{dashboard.name}}</p>
  <p><strong>Description:</strong> {{dashboard.description}}</p>
  <button (click)="nextStep()">Create</button>
</div>


---

📦 4. Dashboard Service

dashboard.service.ts

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


---

✅ 5. Main App Component or Sidebar Action

In your main app or sidebar component, you can show ManageDashboardComponent when "Manage Dashboard" is clicked.


---

Let me know if you'd like this turned into a working StackBlitz or want to use Angular Material components for a better UI.


