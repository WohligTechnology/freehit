# THREE.js BASICS

#### Import javascript files we need

1. `<script src="js/three.js" charset="utf-8"></script>`
2. `<script src="js/jquery.min.js" charset="utf-8"></script>`
3. `<script src="js/OrbitControls.js" charset="utf-8"></script>`
4. `<script src="js/OBJLoader.js" charset="utf-8"></script>`

#### Creating a scene

`var scene = new THREE.Scene();`  
`var width = window.innerWidth;`  
`var height = window.innerHeight;`


#### Creating a render
`var renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });`   
`renderer.setSize(width, height);`  
`document.body.appendChild(renderer.domElement);`   
`renderer.setClearColor(0xffffff, 1);`  
`renderer.recieveShadow = true;`

#### Creating a camera
`var camera = new THREE.PerspectiveCamera(45, width / height, 0.1, 10000);`
`camera.position.set(0, 4, 8);`   
`scene.add(camera);`

#### Adding controls
`var controls = new THREE.OrbitControls(camera, renderer.domElement);`  
`controls.enableRotate = true;`   
`controls.enableZoom = false;`

#### Updating / Resizing viewport (if needed)
`window.addEventListener('resize', function() {`  
  `renderer.setSize(width, height);`  
  `camera.aspect = width / height;`   
  `camera.updateProjectionMatrix();`  
`});`

#### Adding lights
`var ambientLight = new THREE.AmbientLight(0xffffff);`    
`scene.add(ambientLight);`

`var directionalLight = new THREE.DirectionalLight(0xffffff, 0.5);`   
`directionalLight.shadowCameraNear = 1;`    
`directionalLight.shadowCameraFar = 150;`   
`directionalLight.castshadow = true;`   
`scene.add(directionalLight);`

`var spotLight = new THREE.SpotLight(0xffffff);`    
`spotLight.position.set(1000, 1000, 1000);`   
`spotLight.castShadow = true;`    
`camera.add(spotLight);`

#### Creating Native Sphere

`var geometry = new THREE.SphereGeometry(1, 50, 50);`   
`var texture = new THREE.TextureLoader();`   
`texture.load(`    
  `<insert texture here>,`    
  `function(texture) {`   
    `var material = new THREE.MeshPhongMaterial({ map: texture });`   
    `var sphere = new THREE.Mesh(geometry, material);`    
    `sphere.castShadow = true;`   
    `sphere.rotation.y = -5.5;`   
    `sphere.rotation.z = -1;`   
    `scene.add(sphere); },`    
  `function(xhr) { console.log((xhr.loaded / xhr.total * 100) + '% loaded'); },`    
  `function(xhr) { console.log('An error happened'); }`   
`);`

#### Loading JSON

`var loader = new THREE.JSONLoader();`    
`loader.load('<insert json here>', function(geometry) {`        
  `var texture = THREE.ImageUtils.loadTexture("<insert texture here>");`      
  `texture.wrapS = THREE.RepeatWrapping;`   
  `texture.wrapT = THREE.RepeatWrapping;`   
  `material = new THREE.MeshBasicMaterial({ map: texture });`   
  `var mesh = new THREE.Mesh(geometry, material);`    
  `var model = new THREE.Object3D();`   
  `model.add(mesh);`    
  `scene.add(model);`   
`});`

#### Animate Renderer

`function animate() {`    
  `requestAnimationFrame(animate);`    
  `renderer.render(scene, camera); `    
`}`
