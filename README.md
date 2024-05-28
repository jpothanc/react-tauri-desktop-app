# Build Web Desktop Apps using Tauri

Tauri is a toolkit for developing desktop applications with web frontends. It allows you to compile web apps into native applications on Windows, macOS, and Linux. Tauri integrates with the front-end framework of your choice, whether it's React, Vue, Svelte, or even vanilla JavaScript. Developers create their user interface as if designing a regular web application. Tauri then acts as a bridge, converting this web content into a native application. it is a minimalistic, performant and more secure alternative to other similar tools like Electron.
My goal here is to demonstrate how you can build your first Tauri app using React and Vite in Windows.

### Prerequisites

Node.js: Required for managing the development toolchain.
Rust: As Tauri compiles to Rust, having the Rust toolchain installed via rustup is essential.
Webview2 (for Windows users): Necessary for rendering web content in Tauri apps on Windows platforms. If you have Microsoft Edge installed on your system, you do not need to separately install WebView2 for Tauri applications on Windows.

### Tauri stand-alone app in 10 steps

```c
//Install node.js and rust and check thier versions
1. check node and rest versions using node -v and rustc --version commands

//Install Tauri CLI.The is essential for initializing
//new Tauri projects, building, and managing the development process.
2. npm install @tauri-apps/cli

//Create react app called my-first-tauri-app using vite
3. npm create vite@latest react-tauri-desktop-app -- --template react-ts
4. cd my-tauri-app
5. npm install

//Initializes a new Tauri project within your existing web application.
//It sets up the necessary Tauri configuration files and directories
//in your project. Press enter and accept the defaults.code
6. npx tauri init

C:\Projects\React\react-tauri-desktop-app>npx tauri init
✔ What is your app name? · react-tauri-desktop-app
✔ What should the window title be? · react-tauri-desktop-app
? Where are your web assets (HTML/CSS/JS) located, relative to the "<current dir>/src-tauri/tauri.conf.json" file that w✔ Where are your web assets (HTML/CSS/JS) located, relative to the "<current dir>/src-tauri/tauri.conf.json" file that will be created? · ../build
✔ What is the url of your dev server? · http://localhost:3000
✔ What is your frontend dev command? · npm run dev
✔ What is your frontend build command? · npm run build

// Open the react app in VS Code
7. code .

//Edit vite.config.ts to override the port to 3000
8. By default react app runs on 5173, we need to override this to 3000
   To do this, open vite.config.ts and add the server and port options.
    export default defineConfig({
      plugins: [react()],
      server:{
        port: 3000,
      }
    })

//Edit tauri.conf.json
9. Change distDir from ../build to ../dist and identifier option.
"build": {
    ....
    "distDir": "../dist"
  },
  ....
// It cannot be the default(com.tauri.dev)
// if you don't change this, npx tauri build command will give following error.
// ***Error You must change the bundle identifier in `tauri.conf.json > tauri > bundle
// > identifier`. The default value `com.tauri.dev` is not allowed as it must
// be unique across applications.***
 "identifier": "com.example.tauri",

//bring up the standalone app
10. npx tauri dev
```

### Building and Running as an executable

npx tauri build
//This will create the release package \src-tauri\target\release folder.
//click react-tauri-desktop-app to run the application
