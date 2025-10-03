Created: 2025-10-03 13:58
## Family Tree:
1. [[ThreeJS]]
-- -
## Basic Files
Every three.js project needs at least one HTML file to define the webpage, and a JavaScript file to run your three.js code. The structure and naming choices below aren't required, but will be used throughout this guide for consistency.
`index.html`:
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>My first three.js app</title>
    <style>
      body { margin: 0; }
    </style>
  </head>
  <body>
    <script type="module" src="/main.js"></script>
  </body>
</html>
```
`main.js`:
```js
import * as THREE from 'three';
```
`public/`:
The _public/_ folder is sometimes also called a "static" folder, because the files it contains are pushed to the website unchanged. Usually textures, audio, and 3D models will go here.
## Installation and Development
Now that we've set up the basic project structure, we need a way to run the project locally and access it through a web browser. Installation and local development can be accomplished with npm and a build tool, or by importing three.js from a CDN. Both options are explained in the sections below.
### Install with NPM and a build tool
#### Development
Installing from the npm package registry and using a build tool is the recommended approach for most users — the more dependencies your project needs, the more likely you are to run into problems that the static hosting cannot easily resolve. With a build tool, importing local JavaScript files and npm packages should work out of the box, without import maps.
1. Install Node.js. We'll need it to load manage dependencies and to run our build tool.
2. Install three.js and a build tool, Vite, using a terminal in your project folder. Vite will be used during development, but it isn't part of the final webpage. If you prefer to use another build tool, that's fine — we support modern build tools that can import ES Modules.
```sh
# three.js
npm install --save three

# vite
npm install --save-dev vite
```
3. From your terminal, run: `npx vite`
4. If everything went well, you'll see a URL like http://localhost:5173 appear in your terminal, and can open that URL to see your web application.
#### Production
Later, when you're ready to deploy your web application, you'll just need to tell Vite to run a production build — _npx vite build_. Everything used by the application will be compiled, optimized, and copied into the _dist/_ folder. The contents of that folder are ready to be hosted on your website.
## Addons
Out of the box, three.js includes the fundamentals of a 3D engine. Other three.js components — such as controls, loaders, and post-processing effects — are part of the `addons/` directory. Addons do not need to be _installed_ separately, but do need to be _imported_ separately.
The example below shows how to import three.js with the `OrbitControls` and `GLTFLoader` addons. Where necessary, this will also be mentioned in each addon's documentation or examples.
```js
import * as THREE from 'three';
import { OrbitControls } from 'three/addons/controls/OrbitControls.js';
import { GLTFLoader } from 'three/addons/loaders/GLTFLoader.js';

const controls = new OrbitControls( camera, renderer.domElement );
const loader = new GLTFLoader();
```