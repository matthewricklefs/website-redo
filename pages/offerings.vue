<template>
  <div id="offerings" v-bind:class="[animation ? animationClass : '']">
    <NavBar
      class="is-sticky"
      v-bind:style="{ top: topPosition + 'px' }"
    ></NavBar>
    <h1>Service Offerings</h1>
    <canvas
      id="canvas-background"
      :width="getWidth()"
      :height="getHeight()"
    ></canvas>
    <Offerings
      :serviceOfferings="serviceOfferings"
      v-on:offering-clicked="animateBackground"
    />
    <div class="call-to-action">
      <b-row>
        <b-col>
          <router-link to="Onboarding">
            <b-button variant="outline-primary">READY TO LEVEL UP</b-button>
          </router-link>
        </b-col>
      </b-row>
    </div>
    <Footer></Footer>
  </div>
</template>
<script>
import NavBar from "../components/NavBar.vue";
import sourceCodeImage from "../assets/SourceCode.png";
import corporateFutureImage from "../assets/corporate-future.png";
import activitiesKeyboardImage from "../assets/KeyboardKeys.jpg";
import Offerings from "../components/Offerings.vue";
import Footer from "../components/Footer.vue";
export default {
  components: {
    NavBar,
    Offerings,
    Footer,
  },
  data() {
    return {
      serviceOfferings: [
        {
          image: sourceCodeImage,
          title: "Technology Advisement",
          content: [
            "Expert guidance on using technologies that best fit your needs",
            "",
            "1. Our Technology Consultation agreements focus time on aligning your business strategies with available technologies.",
            "2. Multiple Identified technologies are preseneted with estimations on difficulty of use, availability, and requirements.",
            "3. Upon choosing a technology avenue, we then proceed with a minimum viable or demonstration release.",
            "4. You evaluate the release.",
            "5a. Upon success we prepare the release for product development and full incorporation plans can begin.",
            "5b. Alternativley another technology avenue is chosen if your business strategy has not changed.",
          ],
          class: "mb-2",
          animation: "tech",
          show: null,
          collapseId: "1",
        },
        {
          image: corporateFutureImage,
          title: "Product Development Strategem",
          content: [
            "Use our expertise to design products and ensure a solid solution lifecycle",
            "",
            "1. Our Product Consultation agreements start with an allotment of time to scope and ascertain your unique needs.",
            "2. We then present solution architectures based on your priorities and objectives, complete with scheamtics and plans.",
            "3a. At this stage you can choose to take the plans and have another team execute.",
            "3b. Alterantivley we can help coordinate and service the solution's development.",
          ],
          class: "mb-1",
          //id: "mid-card",
          animation: "corporate",
          show: null,
          collapseId: "2",
        },
        // {
        //   image: activitiesKeyboardImage,
        //   title: 'Business Operations',
        //   content: [
        //     'Tech-enable your key activities for maximum efficiency and scalability',
        //     'ASSUMPTIONS',
        //     ''
        //   ],
        //   class: "mb-2",
        //   animation: "business",
        //   show: null,
        //   collapseId: '3'
        // }
      ],
      animation: false,
      animationBackground: null,
      animationClass: null,
      topPosition: 0,
    };
  },
  methods: {
    handleScroll() {
      this.topPosition = window.scrollY;
    },
    getWidth() {
      return window.screen.width;
    },
    getHeight() {
      return window.screen.height;
    },
    animateBackground(id) {
      console.log("animateBackground", id);
      if (id === "Technology Advisement") {
        this.animationClass = "anim1";
        this.serviceOfferings[0].show = true;
        this.animationTech();
      } else if (id === "Product Development Strategem") {
        this.animationClass = "anim2";
        this.serviceOfferings[1].show = true;
        this.animationCorporate();
      } else if (id === "Business Operations") {
        this.serviceOfferings[2].show = true;
        this.animationClass = "anim3";
      }
      this.animation = true;
    },
    animationTech() {
      var canvas = document.getElementById("canvas-background");
      // canvas.style.width = `${window.innerWidth}px`;
      // canvas.style.height = `${window.innerHeight}px`;
      // console.log('animationNetwork', canvas.style.width, canvas.style.height)
      var ctx = canvas.getContext("2d");
      var circles = [];
      this.animationBackground = "#80bfff";
      for (var i = 0; i < canvas.width / 10 + canvas.height / 10; i++) {
        var c = new Circle(
          getRandomInteger(1, canvas.width),
          getRandomInteger(1, canvas.height),
          2,
          getRandomDecimal(-1, 1),
          getRandomDecimal(-1, 1)
        );
        circles.push(c);
      }

      // Random number generator between two numbers
      function getRandomDecimal(min, max) {
        return Math.random() * (max - min) + min;
      }

      // Random integer generator between two numbers
      function getRandomInteger(min, max) {
        return Math.floor(Math.random() * (max - min) + min);
      }

      // Circle object
      //  parameters
      //      x and y are the initial positions
      //      rad is the radius
      //      vx and vy are the component speeds
      function Circle(x, y, rad, vx, vy) {
        var _this = this;

        // constructor
        (function () {
          _this.x = x || null;
          _this.y = y || null;
          _this.radius = rad || null;
          _this.vx = vx || null;
          _this.vy = vy || null;
        })();

        // update function, this will make the circles appear like they are moving.
        this.update = function () {
          _this.x += _this.vx;
          _this.y += _this.vy;

          // these if statments below are what cause the cirlce to appear on the other side of the simulation when they seem to go off screen.
          if (_this.x > canvas.width + _this.radius) {
            _this.x = 0 + _this.radius;
          }
          if (_this.y > canvas.height + _this.radius) {
            _this.y = 0 + _this.radius;
          }
          if (_this.x < 0 + this.radius) {
            _this.x = canvas.width - _this.radius;
          }
          if (_this.y < 0 + _this.radius) {
            _this.y = canvas.height - _this.radius;
          }
        };

        // this method will allow each circle to request the browser to draw it on the screen.
        this.draw = function (ctx, color) {
          if (!_this.x || !_this.y || !_this.radius || !_this.vx || !_this.vy) {
            console.error("Circle requires an x, y, radius, vx and vy");
            return;
          }
          ctx.beginPath();
          ctx.arc(_this.x, _this.y, _this.radius, 0, 2 * Math.PI, false);
          ctx.fillStyle = color;
          ctx.fill();
          // Build an array of all other circles that are within 25px of the current circles and draw a line between that circle and this one
          var neighbors = [];
          for (var i = 0; i < circles.length; i++) {
            // this is what filters what circles are considered neighbors and which ones are not relative to the current cirlce being rendered in frame.
            if (
              Math.abs(circles[i].x - _this.x) < canvas.height / 40 &&
              Math.abs(circles[i].y - _this.y) < canvas.width / 40 &&
              circles[i].x - _this.x != 0 &&
              circles[i].y - _this.y != 0
            ) {
              neighbors.push(circles[i]);
            }
          }
          // for each neighbor to this cirlce being rendered draw a line.
          for (var i = 0; i < neighbors.length; i++) {
            ctx.moveTo(_this.x, _this.y);
            ctx.lineTo(neighbors[i].x, neighbors[i].y);
            ctx.strokeStyle = color;
            ctx.stroke();
          }
        };
      }

      // animation loop
      function loop() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        for (var i = 0; i < circles.length; i++) {
          circles[i].update();
          circles[i].draw(ctx, "#b3d9ff");
        }
        requestAnimationFrame(loop);
      }

      // start the loop
      loop();
    },
    animationCorporate() {
      /* objectives
       *  we will have m number of points arranged circularly.
       *  we can store these points in cartesian x and y points numbered 0 - n
       *  we will have one set m number of lines drawn and another set of m * scalar which will correspond too one of the enumerated points around the circle
       *  EXAMPLE:
       *       start with initial point 1 at position (cos(1 * 2 * pi / 200) * radius, sin(1 * 2 * pi / 200) * radius)
       *       multiplied by two will go to point 2 at position (cos(2 * 2 * pi / 200) * radius, sin(2 * 2 * pi / 200) * radius)
       *       multiply from there by two to get to point 4 at position (cos(4 * 2 * pi / 200) * radius, sin(4 * 2 * pi / 200) * radius)
       */

      /* This function will return an array of x y coordinates that divide the arcs that trace the circumference of a circle.
       *  parameters:
       *       x_center : is the center of the circle's x position.
       *       y_center : is the center of the circle's y position.
       *       amount : is the amount of points to generate.
       *       radius : is the radius of the circle to use to compute the points.
       */
      var updateSelector = Math.floor(Math.random() * 7);
      console.log("updateSelector", updateSelector);
      function line_multiplied(args) {
        var _this = this;
        // Index position of begining point
        var index = args[0];
        // origin x of circle
        var x_center = args[1] || null;
        // origin y of circle
        var y_center = args[2] || null;
        // radius of circle
        var r = args[3] || null;
        // total number of points
        var total_points = args[4] || null;
        // scalar to multiply by
        var s = args[5] || null;

        // constructor, that is made from a closure in javascript. A self executing method that runs when the function line_multiplied() is invoked.
        (function () {
          // Index position of begining point
          _this.index = index;
          // origin x of circle
          _this.x_center = x_center || null;
          // origin y of circle
          _this.y_center = y_center || null;
          // radius of circle
          _this.r = r || null;
          // total number of points
          _this.total_points = total_points || null;
          // scalar to multiply by
          _this.s = s || null;
          // x position first line will end on, reflected will begin from
          //_this.x0 = (_this.x_center + _this.r * Math.cos(2 * Math.PI * _this.index / _this.total_points));
          _this.x0 =
            _this.x_center +
            _this.r *
              Math.cos((2 * Math.PI * _this.index) / _this.total_points);
          // y position first line will end on, reflected will begin from
          //_this.y0 = (_this.y_center + _this.r * Math.sin(2 * Math.PI * _this.index / _this.total_points));
          _this.y0 =
            _this.y_center +
            _this.r *
              Math.sin((2 * Math.PI * _this.index) / _this.total_points);
          // x position reflected line will end at
          //_this.xm = (_this.x0 + _this.r * Math.cos(_this.s * 2 * Math.PI * _this.index / _this.total_points));
          _this.xm =
            _this.x0 +
            _this.r *
              Math.cos(
                (_this.s * 2 * Math.PI * _this.index) / _this.total_points
              );
          // y position reflected line will end at
          //_this.ym = (_this.y0 + _this.r * Math.sin(_this.s * 2 * Math.PI * _this.index / _this.total_points));
          _this.ym =
            _this.y0 +
            _this.r *
              Math.sin(
                (_this.s * 2 * Math.PI * _this.index) / _this.total_points
              );
        })();

        function update1() {
          // increment scalar
          _this.s += 0.005;
          // x position first line will end on, reflected will begin from
          _this.x0 =
            _this.x_center +
            _this.r *
              Math.cos((2 * Math.PI * _this.index) / _this.total_points);
          // y position first line will end on, reflected will begin from
          _this.y0 =
            _this.y_center +
            _this.r *
              Math.sin((2 * Math.PI * _this.index) / _this.total_points);
          // x position reflected line will end at
          _this.xm =
            _this.x0 +
            _this.r *
              Math.cos(
                (_this.s * 2 * Math.PI * _this.index) / _this.total_points
              );
          // y position reflected line will end at
          _this.ym =
            _this.y0 +
            _this.r *
              Math.sin(
                (_this.s * 2 * Math.PI * _this.index) / _this.total_points
              );
        }

        function update2() {
          // increment scalar
          _this.s += 0.005;
          // x position first line will end on, reflected will begin from
          _this.x0 =
            _this.x_center +
            _this.r *
              Math.cos((2 * Math.PI * _this.index) / _this.total_points);
          // y position first line will end on, reflected will begin from
          _this.y0 =
            _this.y_center +
            _this.r *
              Math.sin((2 * Math.PI * _this.index) / _this.total_points);
          // x position reflected line will end at
          _this.xm =
            _this.x0 +
            ((_this.r *
              Math.cos(
                (_this.s * 2 * Math.PI * _this.index) / _this.total_points
              )) %
              2);
          // y position reflected line will end at
          _this.ym =
            _this.y0 +
            _this.r *
              Math.sin(
                (_this.s * 2 * Math.PI * _this.index) / _this.total_points
              );
        }

        function update3() {
          // increment scalar
          _this.s += 0.005;
          // x position first line will end on, reflected will begin from
          _this.x0 =
            _this.x_center +
            _this.r *
              Math.cos((2 * Math.PI * _this.index) / _this.total_points);
          // y position first line will end on, reflected will begin from
          _this.y0 =
            _this.y_center +
            _this.r *
              Math.sin((2 * Math.PI * _this.index) / _this.total_points);
          // x position reflected line will end at
          _this.xm =
            _this.x0 +
            _this.r *
              Math.cos(
                (_this.s * 2 * Math.PI * _this.index) / _this.total_points
              );
          // y position reflected line will end at
          _this.ym =
            _this.y0 +
            ((_this.r *
              Math.sin(
                (_this.s * 2 * Math.PI * _this.index) / _this.total_points
              )) %
              2);
        }

        function update4() {
          // increment scalar
          _this.s += 0.005;
          // x position first line will end on, reflected will begin from
          _this.x0 =
            _this.x_center +
            ((_this.r *
              Math.cos((2 * Math.PI * _this.index) / _this.total_points)) %
              2);
          // y position first line will end on, reflected will begin from
          _this.y0 =
            _this.y_center +
            _this.r *
              Math.sin((2 * Math.PI * _this.index) / _this.total_points);
          // x position reflected line will end at
          _this.xm =
            _this.x0 +
            _this.r *
              Math.cos(
                (_this.s * 2 * Math.PI * _this.index) / _this.total_points
              );
          // y position reflected line will end at
          _this.ym =
            _this.y0 +
            _this.r *
              Math.sin(
                (_this.s * 2 * Math.PI * _this.index) / _this.total_points
              );
        }

        function update5() {
          // increment scalar
          _this.s += 0.005;
          // x position first line will end on, reflected will begin from
          _this.x0 =
            _this.x_center +
            _this.r *
              Math.cos((2 * Math.PI * _this.index) / _this.total_points);
          // y position first line will end on, reflected will begin from
          _this.y0 =
            _this.y_center +
            _this.r *
              Math.sin((2 * Math.PI * _this.index) / _this.total_points);
          // x position reflected line will end at
          _this.xm =
            _this.x0 +
            _this.r *
              Math.cos(
                (_this.s * 1 * Math.PI * _this.index) / _this.total_points
              );
          // y position reflected line will end at
          _this.ym =
            _this.y0 +
            _this.r *
              Math.sin(
                (_this.s * 2 * Math.PI * _this.index) / _this.total_points
              );
        }

        function update6() {
          // increment scalar
          _this.s += 0.005;
          // x position first line will end on, reflected will begin from
          _this.x0 =
            _this.x_center +
            ((_this.r *
              Math.cos((2 * Math.PI * _this.index) / _this.total_points)) %
              2);
          // y position first line will end on, reflected will begin from
          _this.y0 =
            _this.y_center +
            _this.r *
              Math.sin((2 * Math.PI * _this.index) / _this.total_points);
          // x position reflected line will end at
          _this.xm =
            _this.x0 +
            _this.r *
              Math.cos(
                (_this.s * 2 * Math.PI * _this.index) / _this.total_points
              );
          // y position reflected line will end at
          _this.ym =
            _this.y0 +
            ((_this.r *
              Math.sin(
                (_this.s * 2 * Math.PI * _this.index) / _this.total_points
              )) %
              2);
        }

        function update7() {
          // increment scalar
          _this.s += 0.005;
          // x position first line will end on, reflected will begin from
          _this.x0 =
            _this.x_center +
            _this.r *
              Math.cos((2 * Math.PI * _this.index) / _this.total_points);
          // y position first line will end on, reflected will begin from
          _this.y0 =
            _this.y_center +
            ((_this.r *
              Math.sin((2 * Math.PI * _this.index) / _this.total_points)) %
              2);
          // x position reflected line will end at
          _this.xm =
            _this.x0 +
            _this.r *
              Math.cos(
                (_this.s * 2 * Math.PI * _this.index) / _this.total_points
              );
          // y position reflected line will end at
          _this.ym =
            _this.y0 +
            _this.r *
              Math.sin(
                (_this.s * 2 * Math.PI * _this.index) / _this.total_points
              );
        }

        var updates = [
          update1,
          update2,
          update3,
          update4,
          update5,
          update6,
          update7,
        ];

        // update function
        this.update = function () {
          return updates[updateSelector]();
        };

        this.draw = function (ctx) {
          ctx.beginPath();
          ctx.moveTo(_this.x0, _this.y0);
          ctx.lineTo(_this.xm, _this.ym);
          ctx.strokeStyle = "#cccccc";
          ctx.lineWidth = 1;
          ctx.stroke();
        };
      }
      /*
        window.onload = function () {
            document.getElementById('canvas').width = window.innerWidth;
            document.getElementById('canvas').height = window.innerHeight;
        }
        */
      var canvas = document.getElementById("canvas-background");
      var ctx = canvas.getContext("2d");
      var points = [];
      for (var i = 0; i < 300; i++) {
        points.push(
          new line_multiplied([
            i,
            canvas.width / 4,
            canvas.height / 3,
            canvas.width / 8,
            300,
            0.001,
          ])
        );
      }

      // animation loop
      function loop() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        for (var i = 0; i < 300; i++) {
          points[i].update();
          points[i].draw(ctx);
          //console.log(points[i]);
        }
        requestAnimationFrame(loop);
      }
      // call loop
      loop();
    },
  },
  mounted() {
    window.addEventListener("scroll", this.handleScroll);
  },
  beforeDestroy() {
    window.removeEventListener("scroll", this.handleScroll);
  },
};
</script>
