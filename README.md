🧩 Micro Frontend Architecture – Angular 19 + Module Federation

This repo contains a Micro Frontend setup using Angular 19 and Webpack Module Federation. It consists of:

Shell / Container (Main host app)

Remote 1: mfe-header

Remote 2: mfe-dashboard

![image](https://github.com/user-attachments/assets/c66a6ea4-9aac-4ef0-8ed3-ec7bb99c4f71)


🚀 Getting Started
Install dependencies in all projects:

npm install
Run the apps in separate terminals:

# Run mfe-header on port 4201
cd mfe-header
ng serve --port 4201

# Run mfe-dashboard on port 4202
cd mfe-dashboard
ng serve --port 4202

# Run shell app on port 4200
cd shell
ng serve --port 4200

⚙️ Module Federation Configuration
webpack.config.js (example for mfe-header)

exposes: {
  './Component': './projects/mfe-header/src/app/app.component.ts',
}

Shell app.routes.ts:

{
    path: 'header',
    loadComponent: () =>
      loadRemoteModule({
        type: 'module',
        remoteEntry: 'http://localhost:4201/remoteEntry.js',
        exposedModule: './Component', // AppComponent from mfe-header
      }).then((m) => m.AppComponent),
  },

🧪 Test It

Open the shell app:
http://localhost:4200/header

http://localhost:4200/dashboard

Each route dynamically loads its respective remote.

🛠️ Tools Used


 1) Angular 19

 2) Webpack 5

 3) @angular-architects/module-federation

 4) Standalone Components

 5) Vite (optional, for faster builds)

📌 Tips


Make sure all MFEs expose standalone components using standalone: true

Use loadComponent() instead of loadChildren() when exposing components directly

Shared dependencies must be singleton to avoid version mismatch issues

📚 References


Angular Module Federation Docs

Webpack Module Federation


