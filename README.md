src/
├── app/
│   ├── components/
│   │   ├── top-bar/
│   │   │   ├── top-bar.component.ts
│   │   │   ├── top-bar.component.html
│   │   │   └── top-bar.component.css
│   │   ├── screen-container/
│   │   │   ├── screen-container.component.ts
│   │   │   ├── screen-container.component.html
│   │   │   └── screen-container.component.css
│   │   └── footer/
│   │       ├── footer.component.ts
│   │       ├── footer.component.html
│   │       └── footer.component.css
│   ├── app.component.ts
│   ├── app.component.html
│   └── app.module.ts
└── styles.css


 top-bar.component.html//header
 <!-- src/app/components/top-bar/top-bar.component.html -->
<div class="top-bar" role="banner" aria-label="Top navigation bar">
  <img
    src="https://storage.googleapis.com/a1aa/image/d09e78b5-18a4-4c00-5079-5569b1fce13e.jpg"
    alt="BNP PARIBAS logo green square with white letters BNP"
    width="24"
    height="24"
    aria-hidden="true"
  />
  <span>BNP PARIBAS</span>
  <span class="italic font-semibold">NextGen Recon</span>
</div>

header.comp.ts no cahnge

header.comp.css
/* src/app/components/top-bar/top-bar.component.css */
.top-bar {
  background-color: #1a4d2e;
  width: 100%;
  max-width: 960px;
  border-radius: 0.5rem 0.5rem 0 0;
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 0.5rem 1rem;
  box-sizing: border-box;
  user-select: none;
  color: #a3d9a5;
  font-weight: 600;
  font-size: 0.875rem;
  font-style: italic;
  box-shadow: 0 2px 6px rgb(0 0 0 / 0.3);
}
.top-bar img {
  width: 24px;
  height: 24px;
}

login.comp.ts
// src/app/components/screen-container/screen-container.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-screen-container',
  templateUrl: './screen-container.component.html',
  styleUrls: ['./screen-container.component.css']
})
export class ScreenContainerComponent {
  uid: string = '';
  password: string = '';

  onSubmit() {
    alert('Login submitted');
  }

  onSSOLogin() {
    alert('SSO login clicked');
  }
}

login.comp.html
<!-- src/app/components/screen-container/screen-container.component.html -->
<div class="screen-container" role="main" aria-label="NextGen Recon main content">
  <div class="boxes-wrapper flex flex-wrap gap-8">
    <!-- Online Documentation Box -->
    <section
      class="box"
      tabindex="0"
      aria-labelledby="doc-title"
      aria-describedby="doc-desc"
    >
      <h2 id="doc-title">Online Documentation</h2>
      <p id="doc-desc">
        Access comprehensive guides and manuals to help you navigate and
        utilize NextGen Recon features efficiently.
      </p>
      <a
        href="#"
        class="text-green-700 font-semibold underline"
        aria-label="Go to Online Documentation"
      >
        Explore Docs <i class="fas fa-arrow-right ml-1"></i>
      </a>
    </section>

    <!-- Video Tutorial Box -->
    <section
      class="box"
      tabindex="0"
      aria-labelledby="video-title"
      aria-describedby="video-desc"
    >
      <h2 id="video-title">Video Tutorials</h2>
      <p id="video-desc">
        Watch step-by-step video tutorials to get hands-on training and quick
        tips for mastering NextGen Recon.
      </p>
      <a
        href="#"
        class="text-green-700 font-semibold underline"
        aria-label="Go to Video Tutorials"
      >
        Watch Videos <i class="fas fa-play ml-1"></i>
      </a>
    </section>

    <!-- Login Box -->
    <section
      class="box"
      tabindex="0"
      aria-labelledby="login-title"
      aria-describedby="login-desc"
      role="form"
      aria-live="polite"
    >
      <h2 id="login-title">Login</h2>
      <p id="login-desc" class="mb-4 text-green-800 font-semibold italic">
        Reconciliation &amp; Trade Matching
      </p>
      <form
        class="w-full max-w-xs mx-auto"
        (ngSubmit)="onSubmit()"
        aria-label="Login form"
      >
        <input
          type="text"
          placeholder="UID"
          class="login-input"
          [(ngModel)]="uid"
          name="uid"
          aria-required="true"
          aria-label="User ID"
          autocomplete="username"
          required
        />
        <input
          type="password"
          placeholder="Password"
          class="login-input"
          [(ngModel)]="password"
          name="password"
          aria-required="true"
          aria-label="Password"
          autocomplete="current-password"
          required
        />
        <button
          type="submit"
          class="login-button mt-4"
          aria-label="Submit login form"
        >
          Submit
        </button>
      </form>
      <p class="mt-3 text-xs text-green-700 italic opacity-70">or</p>
      <button
        type="button"
        class="mt-1 text-green-700 underline text-xs"
        aria-label="Login with Single Sign-On"
        (click)="onSSOLogin()"
      >
        Login with SSO
      </button>
    </section>
  </div>
</div>

login.comp.css
/* src/app/components/screen-container/screen-container.component.css */
.screen-container {
  background: white;
  border-radius: 0 0 1rem 1rem;
  box-shadow: 0 8px 24px rgb(0 0 0 / 0.15);
  width: 100%;
  max-width: 960px;
  padding: 2rem;
  display: flex;
  flex-wrap: wrap;
  gap: 2rem;
  box-sizing: border-box;
  flex-direction: column;
  margin-bottom: 3rem;
}

.box {
  background: #f0f9f4;
  border: 2px solid #2f855a;
  border-radius: 1rem;
  flex: 1 1 280px;
  min-height: 220px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 1.5rem;
  color: #276749;
  box-sizing: border-box;
  text-align: center;
  transition: background-color 0.3s ease;
}

.box:hover {
  background-color: #c6f6d5;
  cursor: pointer;
}

.box h2 {
  font-weight: 700;
  font-size: 1.25rem;
  margin-bottom: 0.75rem;
}

.box p {
  font-size: 0.9rem;
  line-height: 1.4;
  margin-bottom: 1rem;
}

.login-button {
  background-color: #2f855a;
  color: white;
  font-weight: 600;
  padding: 0.3rem 1rem;
  border-radius: 9999px;
  border: none;
  font-size: 0.8rem;
  letter-spacing:0.5px
}
 


sidebar.comp.ts
import { Component, ViewChild, inject } from '@angular/core';
import { Sidebar } from 'primeng/sidebar';
import { Router } from '@angular/router';

import { CommonModule } from '@angular/common';
import { SidebarModule } from 'primeng/sidebar';
import { ButtonModule } from 'primeng/button';
import { RippleModule } from 'primeng/ripple';
import { AvatarModule } from 'primeng/avatar';
import { StyleClassModule } from 'primeng/styleclass';

@Component({
  selector: 'app-sidebar',
  standalone: true,
  imports: [
    CommonModule,
    SidebarModule,
    ButtonModule,
    RippleModule,
    AvatarModule,
    StyleClassModule
  ],
  templateUrl: './sidebar.component.html',
  styleUrls: ['./sidebar.component.css']
})
export class SidebarComponent {
  router = inject(Router);
  sidebarVisible = false;

  @ViewChild('sidebarRef') sidebarRef!: Sidebar;

  closeCallback(e: any): void {
    this.sidebarRef.close(e);
  }

  navigateToPath(path: string): void {
    this.router.navigateByUrl(path);
  }
}

sidebar.comp.html
<div class="container">
  <div class="card flex justify-content-center">
    <p-sidebar #sidebarRef [(visible)]="sidebarVisible" [modal]="true" position="left" showCloseIcon="false" styleClass="custom-sidebar" baseZIndex="10000">
      <ng-template pTemplate="headless">
        <div class="sidebar-header">
          <span class="app-title">Recon NextGen</span>
          <button pButton icon="pi pi-times" (click)="closeCallback($event)" class="p-button-rounded p-button-text close-btn"></button>
        </div>

        <div class="sidebar-content">
          <ul class="sidebar-menu">
            <li (click)="navigateToPath('home')" pRipple>Home</li>
            <li (click)="navigateToPath('match')" pRipple>Matching</li>
            <li (click)="navigateToPath('dragmatch')" pRipple>Drag Match</li>
            <li class="dropdown">
              <div class="dropdown-toggle" pRipple>
                Reports <i class="pi pi-chevron-down ml-auto"></i>
              </div>
              <ul class="dropdown-menu">
                <li pRipple>Sub Report 1</li>
                <li pRipple>Sub Report 2</li>
              </ul>
            </li>
            <li (click)="navigateToPath('exclusion')" pRipple>Exclusion Rules</li>
            <li pRipple>Updation Rules</li>
            <li pRipple>Summary</li>
          </ul>
        </div>
      </ng-template>
    </p-sidebar>

    <button pButton icon="pi pi-bars" (click)="sidebarVisible = true" class="sidebar-toggle-button hello"></button>
  </div>
</div>

sidebar.comp.css
.container {
  position: fixed;
  top: 50%;
  left: 0;
  transform: translateY(-50%);
  z-index: 2000;
}

.custom-sidebar {
  width: 15rem !important;
  background: #1f2937;
  color: white;
  padding: 1rem;
  transition: all 0.3s ease;
}

.sidebar-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1rem;
}

.app-title {
  font-size: 1.4rem;
  font-weight: bold;
  color: #0ea5e9;
}

.close-btn {
  background: transparent;
  color: white;
}

.sidebar-content {
  max-height: 80vh;
  overflow-y: auto;
}

.sidebar-menu {
  list-style: none;
  padding: 0;
}

.sidebar-menu li {
  padding: 0.75rem 1rem;
  cursor: pointer;
  border-radius: 0.5rem;
  transition: background 0.2s;
}

.sidebar-menu li:hover {
  background: rgba(255, 255, 255, 0.1);
}

.dropdown-toggle {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0.75rem 1rem;
  cursor: pointer;
}

.dropdown-menu {
  list-style: none;
  margin-left: 1rem;
  padding: 0.5rem 0;
  display: none;
  animation: dropdown-slide 0.3s ease-in-out forwards;
}

.dropdown:hover .dropdown-menu {
  display: block;
}

.sidebar-toggle-button.hello {
  background-color: #0ea5e9 !important;
  color: white !important;
  border: none;
  border-radius: 50%;
  width: 3rem;
  height: 3rem;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
  transition: transform 0.3s ease;
}

.sidebar-toggle-button.hello:hover {
  transform: scale(1.1);
}

@keyframes dropdown-slide {
  0% {
    opacity: 0;
    transform: translateY(-5px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}


ts
import { Component } from '@angular/core';
import { Router } from '@angular/router';
import { CommonModule } from '@angular/common';
import { RippleModule } from 'primeng/ripple';

@Component({
  selector: 'app-sidebar',
  standalone: true,
  imports: [CommonModule, RippleModule],
  templateUrl: './sidebar.component.html',
  styleUrls: ['./sidebar.component.css']
})
export class SidebarComponent {
  constructor(private router: Router) {}

  navigateToPath(path: string): void {
    this.router.navigateByUrl(path);
  }
}

html
<div class="static-sidebar">
  <div class="sidebar-header">
    <span class="app-title">Recon NextGen</span>
  </div>

  <div class="sidebar-content">
    <ul class="sidebar-menu">
      <li (click)="navigateToPath('home')" pRipple>Home</li>
      <li (click)="navigateToPath('match')" pRipple>Matching</li>
      <li (click)="navigateToPath('dragmatch')" pRipple>Drag Match</li>
      <li class="dropdown">
        <div class="dropdown-toggle" pRipple>
          Reports <i class="pi pi-chevron-down ml-auto"></i>
        </div>
        <ul class="dropdown-menu">
          <li pRipple>Sub Report 1</li>
          <li pRipple>Sub Report 2</li>
        </ul>
      </li>
      <li (click)="navigateToPath('exclusion')" pRipple>Exclusion Rules</li>
      <li pRipple>Updation Rules</li>
      <li pRipple>Summary</li>
    </ul>
  </div>
</div>

cse
/* [Green and white theme applied below] */
.static-sidebar {
  position: fixed;
  top: 0;
  left: 0;
  height: 100vh;
  width: 15rem;
  background: #ffffff; /* [Changed from dark to white background] */
  color: #2e7d32; /* [Green text] */
  padding: 1rem;
  z-index: 1000;
  overflow-y: auto;
  box-shadow: 2px 0 8px rgba(0, 0, 0, 0.1); /* [Optional visual separation] */
}

.sidebar-header {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 1.5rem;
}

.app-title {
  font-size: 1.5rem;
  font-weight: bold;
  color: #2e7d32; /* [Changed title to green] */
}

.sidebar-content {
  height: calc(100% - 3rem);
}

.sidebar-menu {
  list-style: none;
  padding: 0;
}

.sidebar-menu li {
  padding: 0.75rem 1rem;
  cursor: pointer;
  border-radius: 0.5rem;
  transition: background 0.2s;
  color: #2e7d32; /* [Green menu items] */
}

.sidebar-menu li:hover {
  background: #e8f5e9; /* [Light green hover] */
}

.dropdown-toggle {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0.75rem 1rem;
  cursor: pointer;
  color: #2e7d32; /* [Green dropdown toggle] */
}

.dropdown-menu {
  list-style: none;
  margin-left: 1rem;
  padding: 0.5rem 0;
  display: none;
  animation: dropdown-slide 0.3s ease-in-out forwards;
}

.dropdown:hover .dropdown-menu {
  display: block;
}

.dropdown-menu li {
  color: #2e7d32; /* [Green subitems] */
}

.dropdown-menu li:hover {
  background-color: #f1f8e9; /* [Softer green hover] */
}

@keyframes dropdown-slide {
  0% {
    opacity: 0;
    transform: translateY(-5px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}


-----------------
model/ParseRequest.java
package com.example.desisparser.model;

public class ParseRequest {
    private String desisData;

    public String getDesisData() {
        return desisData;
    }

    public void setDesisData(String desisData) {
        this.desisData = desisData;
    }
}

service/parse service.java
package com.example.desisparser.service;

import org.springframework.stereotype.Service;
import java.util.*;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

@Service
public class ParseService {

    public String convertToCsv(String desisData) {
        Map<String, String> dataMap = new LinkedHashMap<>();

        // Extract headers from first part (e.g., OP4035)
        String typeNature = desisData.substring(0, 2);
        String siteCode = desisData.substring(2, 6);
        String appCode = desisData.substring(6, 14);
        String instrumentCode = desisData.substring(14, 18);

        dataMap.put("TypeNature", typeNature);
        dataMap.put("SiteCode", siteCode);
        dataMap.put("ApplicationCode", appCode);
        dataMap.put("InstrumentCode", instrumentCode);

        // Regex to match *code:value or code:value patterns
        Pattern pattern = Pattern.compile("[*]?(\\d+):([^:*]+)");
        Matcher matcher = pattern.matcher(desisData);

        while (matcher.find()) {
            String key = matcher.group(1).trim();
            String value = matcher.group(2).trim();
            dataMap.put(key, value);
        }

        // Generate CSV
        StringBuilder csv = new StringBuilder();
        // Header row
        csv.append(String.join(",", dataMap.keySet())).append("\n");
        // Data row
        csv.append(String.join(",", dataMap.values())).append("\n");

        return csv.toString();
    }
}

controller/parser controller.java
package com.example.desisparser.controller;

import com.example.desisparser.model.ParseRequest;
import com.example.desisparser.service.ParseService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api/parse")
public class ParseController {

    @Autowired
    private ParseService parseService;

    @PostMapping("/desis-to-csv")
    public String convertDesisToCsv(@RequestBody ParseRequest request) {
        return parseService.convertToCsv(request.getDesisData());
    }
}

desisparseapplication.java

package com.example.desisparser;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class DesisParserApplication {
    public static void main(String[] args) {
        SpringApplication.run(DesisParserApplication.class, args);
    }
}


Full Updated Spring Boot Code


---

Model: ParseRequest.java

package com.example.desisparser.model;

public class ParseRequest {
    private String desisData;

    public String getDesisData() {
        return desisData;
    }

    public void setDesisData(String desisData) {
        this.desisData = desisData;
    }
}


---

Service: ParseService.java

package com.example.desisparser.service;

import org.springframework.stereotype.Service;

import java.io.ByteArrayInputStream;
import java.io.ByteArrayOutputStream;
import java.io.PrintWriter;
import java.util.LinkedHashMap;
import java.util.Map;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

@Service
public class ParseService {

    public ByteArrayInputStream convertToCsvFile(String desisData) {
        Map<String, String> dataMap = new LinkedHashMap<>();

        // Extract first fields
        dataMap.put("Type Nature", desisData.substring(0, 2));
        dataMap.put("Site Code", desisData.substring(2, 6));
        dataMap.put("Application Code", desisData.substring(6, 14));
        dataMap.put("Instrument Code", desisData.substring(14, 18));

        String remaining = desisData.substring(18);

        // Match all *XX:value or XX:value pairs
        Pattern pattern = Pattern.compile("[*]?(\\d+):([^:*]+)");
        Matcher matcher = pattern.matcher(remaining);

        while (matcher.find()) {
            String key = matcher.group(1).trim();
            String value = matcher.group(2).trim();
            dataMap.put(key, value);
        }

        // Write to CSV in memory
        ByteArrayOutputStream out = new ByteArrayOutputStream();
        PrintWriter writer = new PrintWriter(out);

        // Header
        writer.println(String.join(",", dataMap.keySet()));
        // Values
        writer.println(String.join(",", dataMap.values()));

        writer.flush();
        return new ByteArrayInputStream(out.toByteArray());
    }
}


---

Controller: ParseController.java

package com.example.desisparser.controller;

import com.example.desisparser.model.ParseRequest;
import com.example.desisparser.service.ParseService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.core.io.InputStreamResource;
import org.springframework.http.HttpHeaders;
import org.springframework.http.MediaType;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api/parse")
public class ParseController {

    @Autowired
    private ParseService parseService;

    @PostMapping("/desis-to-csv")
    public ResponseEntity<InputStreamResource> convertDesisToCsv(@RequestBody ParseRequest request) {
        var csvStream = parseService.convertToCsvFile(request.getDesisData());

        HttpHeaders headers = new HttpHeaders();
        headers.add("Content-Disposition", "attachment; filename=desis_data.csv");

        return ResponseEntity.ok()
                .headers(headers)
                .contentType(MediaType.parseMediaType("text/csv"))
                .body(new InputStreamResource(csvStream));
    }
}


---

Main Class: DesisParserApplication.java

package com.example.desisparser;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class DesisParserApplication {
    public static void main(String[] args) {
        SpringApplication.run(DesisParserApplication.class, args);
    }
}





1. Create Controller

Create a new Java class:

> src/main/java/com/example/desisparser/controller/DesisController.java



package com.example.desisparser.controller;

import com.example.desisparser.service.DesisService;
import jakarta.servlet.http.HttpServletResponse;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

import java.io.IOException;

@RestController
@RequestMapping("/api/desis")
public class DesisController {

    @Autowired
    private DesisService desisService;

    @PostMapping("/parse")
    public void parseDesisData(@RequestBody String desisData, HttpServletResponse response) throws IOException {
        desisService.processDesisToCSV(desisData, response);
    }
}


---

2. Create Service

> src/main/java/com/example/desisparser/service/DesisService.java



package com.example.desisparser.service;

import org.springframework.stereotype.Service;

import jakarta.servlet.http.HttpServletResponse;
import java.io.PrintWriter;
import java.util.LinkedHashMap;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

@Service
public class DesisService {

    public void processDesisToCSV(String desisData, HttpServletResponse response) throws java.io.IOException {
        LinkedHashMap<String, String> csvData = new LinkedHashMap<>();

        // Extract header parts
        String typeNature = desisData.substring(0, 2);
        String siteCode = desisData.substring(2, 6);
        String appCode = extractAlpha(desisData.substring(6)).split("[0-9]")[0];
        String rem = desisData.substring(6 + appCode.length());
        String instrumentCode = extractAlpha(rem).split("[0-9]")[0];
        String remainingData = rem.substring(instrumentCode.length());

        csvData.put("type_nature", typeNature);
        csvData.put("site_code", siteCode);
        csvData.put("application_code", appCode);
        csvData.put("instrument_code", instrumentCode);

        // Extract remaining key:value pairs using regex
        Pattern pattern = Pattern.compile("(\\d+):([^\\s*]+)");
        Matcher matcher = pattern.matcher(remainingData);

        while (matcher.find()) {
            csvData.put(matcher.group(1), matcher.group(2));
        }

        // Prepare response for CSV download
        response.setContentType("text/csv");
        response.setHeader("Content-Disposition", "attachment; filename=\"parsed_output.csv\"");
        PrintWriter writer = response.getWriter();

        // Write CSV header
        writer.println(String.join(",", csvData.keySet()));

        // Write CSV values
        writer.println(String.join(",", csvData.values()));

        writer.flush();
        writer.close();
    }

    private String extractAlpha(String input) {
        return input.replaceAll("[^A-Za-z]", "");
    }
}
