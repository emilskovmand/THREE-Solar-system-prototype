# Solar System Prototype

This prototype is a Three.js project showing off my first 5 day journey of using [Three.js](https://threejs.org/).

* No post-processing
* No dependencies
* High-resolution images might slow down load time

## Purpose (Formål)

This is just me learning the fundamentals of [Three.js](https://threejs.org/).

(Danish) Det her er bare mig som vil lære det fundamentale af [Three.js](https://threejs.org/).

## Thoughts throughout the project
I chose this idea for a project because I like learning about space and our solar system, and wanted to use math to create a simulation of our planets orbiting the sun... I succeeded and plan on making this into a small game where you can read about our planets.

I started off by implementing the planets and creating them each like:
```javascript 
var Geometry = new THREE.SphereGeometry(300, 32, 32);
var Material = new THREE.MeshPhongMaterial({
    map: new THREE.TextureLoader().load("YOUR/PATH"),
    alphaMap: new THREE.TextureLoader().load("YOUR/PATH"),
    shininess: 5       
})
var mesh = new THREE.Mesh(Geometry, Material);
mesh.name = "Planet's name";
mesh.position.set(0, 0, 0);

scene.add( mesh );
spheres.push(mesh);
```
But quickly realised this is a messy and long routine, so i created a class that could take parameters for its own Planet, the class is long but take a look from **line 97-263**.

This course of action made it easier to work with and later implement moons and Saturn's rings... which took a bit of reading about 3D modeling and [UV-mapping](https://en.wikipedia.org/wiki/UV_mapping), but here's the code to fix the texture for saturn's rings (To be improved)

```javascript 
 // Fixing Saturn Ring texture
var ringPos = saturnRingsGeometry.attributes.position;
var ringV3 = new THREE.Vector3();
for (let i = 0; i < ringPos.count; i++) {
    ringV3.fromBufferAttribute(ringPos, i);
    saturnRingsGeometry.attributes.uv.setXY(i, ringV3.length() < 84 ? 0 : 1, 1)
}
saturnRingsGeometry.uvsNeedUpdate = true;
```

***Before UV-Mapping***

![Broken Texture](https://imgur.com/KS2k4u9.png)

***After UV-Mapping***

![Fixed Texture](https://imgur.com/TR18JsJ.png)

#### Orbiting *The Sun*

After a few hours of memorizing my Math notes about 3D Vectors and circles I came to a conclusion that the planets doesn't need a perfect circle as their orbital path. 
Instead I created a function that created a 2D vectored polygon, which returned the corners as coordinates for our planets orbital path. 

*h = Sun's coordinate on the x-axis, k = Sun's coordinate on the z-axis, points = Amount of corners (More = Less performance & more precise pathing)*

```javascript
function CircularPointsFormula (radius, h, k, points) {
    let Coordinates = [];
    const piRatio = Math.PI / 180;

    for (let i = 0; i < points; i++) {
        var 
            A = ((360 / points) * i);
            B = 90 - A;
            c = radius;
        var x = c * (Math.sin(A * piRatio)) + h,
            y = c * (Math.cos(A * piRatio)) + k;
        Coordinates.push({
            x: x,
            y: y,
            angle: Math.atan2(y - k, x - h) * (180/ Math.PI) % 360
        });
    }
    return Coordinates;
}
```

## Usage (Anvendelse)
As notes for future implementations of the Three.js library...

(Danish) Som noter for fremtidens implementationer of Three.js biblioteket...

## License
This project is not licensed, free to use all you want!
