<template>
  <div class="container">
    <div class="col1">
      <div class="text">
        <h1>Dima Khudiiash</h1>
          <h3>Front End Developer</h3>
      </div>
    </div>
    <div class="col2">
      <img src="https://res.cloudinary.com/dwslf2mo2/image/upload/v1578937276/zpxand58rzaajg36dci9.jpg" alt="">
    </div>
  </div>
</template>

<script>
const THREE = require('three');
export default {
  name: 'Scene',
  props: {
  },
  data : function(){
    return{
      camera: null,
      scene: null, 
      renderer: null,
      geometry: null, 
      material: null, 
      mesh: null,
      // circleColor : Math.random() * 0x42b983 + 0x42b983,
      circleColor : 5782276.748546636,
    }
  },
  created : function (){
    this.init();
    this.animate();
  },
  methods: {
    init: function() {
      this.camera = new THREE.PerspectiveCamera(
        75,
        window.innerWidth / window.innerHeight,
        1,
        10000
      );

      // pink = 6227769.475878448
      // gold = 5782276.748546636
      // cool position: 20,100,50

      this.camera.position.z = 1000;
      this.scene = new THREE.Scene();
      this.renderer = new THREE.WebGLRenderer({ antialias: true });
      this.renderer.setSize(window.innerWidth, window.innerHeight);
      this.renderer.setClearColor(0xf9f9f9);
      document.body.appendChild(this.renderer.domElement);
      this.camera.lookAt(new THREE.Vector3(1, 1, 1));
      this.geometry = new THREE.BoxGeometry(2, 2, 32);
      this.material = new THREE.MeshStandardMaterial({color: this.color, roughness: 0, metalness: 1});
      console.log(this.circleColor)
      var light = new THREE.DirectionalLight( 0x404040, 60 ); // soft white light
      light.position.set(30,10,50)
      var light2 = new THREE.DirectionalLight( 0x404040, 50 ); // another light
      light2.position.set(-30,-50,250)
      var light3 = new THREE.DirectionalLight( "white", 25 ); // another light
      light3.position.set(-30,-50,-150)
      this.scene.add(light);
      this.scene.add(light2);
      this.scene.add(light3);
      for (var i = 0; i < 280; i++) {
        // this.circleColor = Math.random() * 0x42b983 + 0x42b983;
        this.material = new THREE.MeshStandardMaterial( {
           color: this.circleColor,
           roughness: .11,
           metalness: 1
           } );

        var circle = new THREE.Mesh(this.geometry, this.material);
        circle.position.x = Math.random() * 2500 - 1500;
        circle.position.y = Math.random() * 2500 - 1500;
        circle.position.z = Math.random() * 2500 - 1500;
        
        circle.scale.x = circle.scale.y = Math.random() * 12 + 5;
        this.scene.add( circle );
        this.geometry.vertices.push( new THREE.Vector3( circle.position ) );
      }

      // var line = new THREE.Line( this.geometry, new THREE.LineBasicMaterial( { color: 0xfffffff, opacity: 1 } ) );
      // this.scene.add( line );
    },
    animate: function() {
      requestAnimationFrame(this.animate);
      this.renderer.render( this.scene, this.camera );
      this.renderer.setClearColor("black")
      document.addEventListener( 'mousemove', this.onMouseMove, false );
    },
    onMouseMove : function(event){
      var mouseX = (event.clientX - window.innerWidth/2) / window.innerWidth/2;
      var mouseY = (event.clientY - window.innerHeight/2) / window.innerHeight/2;
      this.camera.position.x = Math.sin(mouseX * Math.PI) * 1000;
      this.camera.position.y = - Math.sin(mouseY * Math.PI) * 1000;
      this.camera.lookAt(new THREE.Vector3(0,0,0));
      this.renderer.render( this.scene, this.camera );
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container{
  margin: calc(50vh - 100px) 0 0;
  text-transform: uppercase;
  color: #ffa0238a;
  position: absolute;
  width: 100%;
}
.container h1{
  margin: 0;
}
.container h3{
  /*Font End Develeper*/
  color: #ffffff48;
  margin-top: 5px;
}
.col1, .col2{
  width: 50%;
  float: left;
}
.col1{
  margin-top: 35px;
  display: flex;
  justify-content: center;
  align-items: center;
}
 .text {
    width: fit-content;
    border-radius: 5px;
    padding: 25px;
  }
.container .col1 img{
  width: 32px;
  margin: 5px;
}
.container .col2 img{
  object-fit: cover; 
  width: 200px;
  height: 200px;
  border-radius: 50%;
}
canvas {
  bottom: 0;
  background: #000;
}
</style>