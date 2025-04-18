This repo contains a Micro Frontend setup using Angular 19 and Webpack Module Federation. It consists of:

Shell / Container (Main host app)

Remote 1: mfe-header

Remote 2: mfe-dashboard

/microfrontends/
├── shell/ # Main container application
├── mfe-header/ # Micro frontend for header
└── mfe-dashboard/ # Micro frontend for dashboard

npm install

# Run mfe-header on port 4201

cd mfe-header
ng serve --port 4201

# Run mfe-dashboard on port 4202

cd mfe-dashboard
ng serve --port 4202

# Run shell app on port 4200

cd shell
ng serve --port 4200

Module Federation Configuration
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
exposedModule: './Component',
}).then(m => m.AppComponent),
}

http://localhost:4200/header
http://localhost:4200/dashboard

🛠️ Tools Used
Angular 19

Webpack 5

@angular-architects/module-federation

Standalone Components

Vite (optional, for faster builds)

Tips
Make sure all MFEs expose standalone components using standalone: true

Use loadComponent() instead of loadChildren() when exposing components directly

Shared dependencies must be singleton to avoid version mismatch issues

📚 References
Angular Module Federation Docs

Webpack Module Federation
