<script>
    import * as THREE from 'three';
    import {browser} from '$app/environment';
    import {GLTFLoader} from 'three/examples/jsm/loaders/GLTFLoader.js';
    import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js'

    if(browser)
    {
        
const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(75, window.innerWidth/window.innerHeight, 0.1, 1000);
camera.position.z = 40
const renderer = new THREE.WebGLRenderer();

renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);


const controls = new OrbitControls( camera, renderer.domElement );

const lightColor = 0xFDB813;

const gltfLoader = new GLTFLoader();

const ambient = new THREE.AmbientLight(lightColor, 5 )
const directionLight = new THREE.DirectionalLight(lightColor, 10);
directionLight.position.set(50, 30, 0)
directionLight.castShadow = true;
directionLight.shadow
const geometry = new THREE.BoxGeometry(2, 2, 2)
const material = new THREE.MeshBasicMaterial({ wireframe: true })
const cube = new THREE.Mesh(geometry, material)
cube.position.set(directionLight.position.x,directionLight.position.y,directionLight.position.z );

let treeObject;

scene.add(directionLight);
scene.add(ambient);
scene.add(cube);
gltfLoader.load('models/savana.glb', (gltf) => {
   scene.add(gltf.scene);
   console.log(gltf);
});

function animate(){
    requestAnimationFrame(animate);
    renderer.render(scene, camera);
     // 3. update controls with a small step value to "power its engines"
    controls.update(0.01)
}
animate();  
}


</script>
