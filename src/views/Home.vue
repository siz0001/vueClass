<template>
  <div class="three3d" ref="canvas">
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import * as THREE from 'three'
import { OrbitControls } from "three/examples/jsm/controls/OrbitControls"

const canvas = ref();
const boxMesh = ref()
const planeMesh = ref()
const spotLight = ref()
const controls = ref()

const windowResize = (renderer, camera) => {
  var callback = () => {
    var rendererSize = { width: window.innerWidth, height: window.innerHeight }
    renderer.setSize(rendererSize.width, rendererSize.height)
    camera.aspect = rendererSize.width / rendererSize.height
    camera.updateProjectionMatrix()
  }
  window.addEventListener('resize', callback, false)
  return callback()
}

const createScene = () => {
  const scene = new THREE.Scene();
  scene.background = new THREE.Color("#111111")
  return scene
}
const scene = createScene();

const createCamera = () => {
  let innerWidth = canvas.value.offsetWidth;
  let innerHeight = canvas.value.offsetHeight;
  const camera = new THREE.PerspectiveCamera(75, innerWidth / innerHeight, 0.1, 1000);
  camera.position.z = 100;
  camera.position.y = 50;
  return { camera, innerWidth, innerHeight };
}

const createRenderer = (camera) => {
  const renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
  renderer.shadowMap.enabled = true;
  renderer.shadowMap.type = THREE.PCFSoftShadowMap;
  canvas.value.appendChild(renderer.domElement)
  windowResize(renderer, camera)
  return renderer
}

const createLight = (scene) => {
  scene.add(new THREE.AmbientLight(0x404040));
  spotLight.value = new THREE.SpotLight(0xffffff);
  spotLight.value.position.set(100, 100, 0)
  spotLight.value.target.position.set(0, 0, 0)
  spotLight.value.castShadow = true;
  scene.add(spotLight.value);
}

const createMeshPlane = (scene) => {
  const plane = new THREE.Mesh(new THREE.PlaneGeometry(100, 100), new THREE.MeshPhongMaterial({
    color: 0xffffff,
    side: THREE.DoubleSide,
    shininess: 0
  }));
  plane.rotateX(3 * Math.PI / 2)
  plane.castShadow = false;
  plane.receiveShadow = true;
  scene.add(plane);
  planeMesh.value = plane
}

const createMeshBox = (scene) => {
  const box = new THREE.Mesh(new THREE.BoxGeometry(10, 10, 10), new THREE.MeshPhongMaterial({
    color: 0xffffff,
  }));
  box.position.x = 0
  box.position.y = 20
  box.position.z = 0
  box.rotateX(3 * Math.PI / 2)
  box.castShadow = true;
  box.receiveShadow = true;
  scene.add(box);
  boxMesh.value = box
}

const handleInit = () => {
  const { camera } = createCamera();
  const renderer = createRenderer(camera)
  controls.value = new OrbitControls(camera, renderer.domElement)
  controls.value.target = new THREE.Vector3(0, 0, 0)
  // controls.value.maxPolarAngle = Math.PI / 2;

  createLight(scene)
  const spotLightHelper = new THREE.SpotLightHelper(spotLight.value);
  scene.add(spotLightHelper);
  
  createMeshPlane(scene)
  createMeshBox(scene)

  const axesHelper = new THREE.AxesHelper(500);
  scene.add(axesHelper);

  function animate() {
    boxMesh.value.rotateX(0.008)
    boxMesh.value.rotateY(0.01)
    boxMesh.value.rotateZ(0.005)
    requestAnimationFrame(animate);
    renderer.render(scene, camera);
  }
  animate();
}

onMounted(async () => {
  handleInit();
})

</script>