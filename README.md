# Solar System Prototype

This prototype is a Three.js project showing off my first 5 day journey of using [Three.js](https://threejs.org/).

* No post-processing
* No dependencies

## Purpose (Formål)

This is just me learning the fundamentals of [Three.js](https://threejs.org/).

(Danish) Det her er bare mig som vil lære det fundamentale af [Three.js](https://threejs.org/).

## Thoughts throughout the project
I started off by implementing the planets and creating them each like:
```javascript 
var Geometry = new THREE.SphereGeometry(300, 32, 32);
var Material = new THREE.MeshPhongMaterial({
    map: new THREE.TextureLoader().load("YOUR/PATH"),
    alphaMap: new THREE.TextureLoader().load("YOUR/PATH"),
    shininess: 5       
})
var mesh = new THREE.Mesh(SunGeometry, SunMaterial);
mesh.name = "Planet name";
sun.position.set(0, 0, 0);

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
*This is before and after:*
![Broken Texture](http://url/to/img.png)
![Fixed Texture](https://imgur.com/TR18JsJ)

## Usage (Anvendelse)
As notes for future implementations of the Three.js library...

(Danish) Som noter for fremtidens implementationer of Three.js biblioteket...

## License
This project is not licensed, free to use all you want!
