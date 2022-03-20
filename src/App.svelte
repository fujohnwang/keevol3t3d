<script>
    import {onMount} from 'svelte';
    import * as THREE from 'three';
    import * as SC from 'svelte-cubed';
    import {GLTFLoader} from 'three/examples/jsm/loaders/GLTFLoader.js';

    const height = 0.3,
        size = 1,
        hover = 3,
        curveSegments = 4,
        bevelThickness = 2,
        bevelSize = 1.5;
    const mirror = true;

    let glbGeometry;
    let glbMaterial;

    let spin = 0;
    SC.onFrame(() => {
        spin += 0.01;
    })

    onMount(() => {
        THREE.Cache.enabled = true;

        const glbLoader = new GLTFLoader();
        glbLoader.load('3t.glb', function (glb) {
            console.log("load glb file successfully.");
            const threeT = glb.scene.children[0]
            console.log("%o", threeT)
            glbGeometry = threeT.geometry;
            glbMaterial = threeT.material;
        })


    })
</script>

<SC.Canvas antialias background={new THREE.Color('#3883F8')} shadows>

    <SC.Mesh geometry={glbGeometry} position={[0, 0, 0]}
             material={glbMaterial} rotation={[0,spin,0]}/>

    <SC.PerspectiveCamera position={[5, 0, 11]}/>
    <SC.OrbitControls enableZoom={true}/>
    <SC.AmbientLight intensity={0.6}/>
    <SC.DirectionalLight intensity={0.6} position={[-2, 3, 2]} shadow={{ mapSize: [2048, 2048] }}/>
</SC.Canvas>

