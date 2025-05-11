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
  letter-spacing:
::contentReference[oaicite:31]{index=31}
 

