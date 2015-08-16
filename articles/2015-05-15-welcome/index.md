
# And so it begins

I don't have much to share for write now but check this out : )

<canvas id=canvas></canvas>
<style type="text/css">
* {
   margin:0; padding:0;
}

html {
   overflow:hidden;
}
</style>

<script type="text/javascript">
window.onload = function() {

   window.requestAnimFrame = (function() {
      return window.requestAnimationFrame ||
         window.webkitRequestAnimationFrame ||
         window.mozRequestAnimationFrame ||
         function(callback) {
            window.setTimeout(callback, 1000 / 60);
         };
   })();

   var canvas = document.getElementById("canvas");
   var ctx = canvas.getContext("2d");

   var arr = [];
   var S = function(x, y, angle) {
      this.x = x;
      this.y = y;
      this.angle = angle;
   }

   var num = 32;
   var x = 0;
   var R,r ;
   var lines = 32;
   /*--------------------------------------*/
   function size() {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
   }

   function bg() {
      ctx.fillStyle = "rgba(255,255,255,1)";
      ctx.fillRect(0, 0, canvas.width, canvas.height);
   }

   function init() {
      var x, y, angle;

      for (var i = 1; i <= num; i++) {
         x = canvas.width / 2;
         y = canvas.height / 2;
         angle = (i / num) * 2 * Math.PI;

         arr.push(new S(x, y, angle));
      }
   }

   function update(i) {
      var s = arr[i];

      s.x = canvas.width / 2 + R * Math.cos(s.angle);
      s.y = canvas.height / 2 + R * Math.sin(s.angle);

      s.angle += Math.PI / 720;

   }

   function draw() {
      var s;
      for (var i = 0; i < arr.length; i++) {
         s = arr[i];

         ctx.strokeStyle = "rgb(100,150,200)";
         ctx.beginPath();
         for (var j = 0; j < lines; j++) {
            ctx.moveTo(s.x, s.y);
            ctx.lineTo(
               s.x + r * Math.cos((j / lines) * 2 * Math.PI+3*x),
               s.y + r * Math.sin((j / lines) * 2 * Math.PI+3*x));
         }
         ctx.stroke();

         update(i);
      }
      x += Math.PI / 1440;
      R = Math.abs(120 * Math.sin(x))+120;
      r = Math.abs(190* Math.cos(x))+10;
   }

   function loop() {
         bg();

         draw();
         requestAnimFrame(loop);
      }
      /*--------------------------------------*/
   window.onresize = size;

   size();
   init();
   loop();
}
</script>