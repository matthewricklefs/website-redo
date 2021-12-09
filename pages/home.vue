<template>
  <div id="home">
    <NavBar class="is-sticky" v-bind:class="[isNavBackground ? backgroundClass : '']"
      v-bind:style="{ top: topPosition + 'px'}"  
    ></NavBar>
    <!-- <div id="test">words</div> -->
    <!-- <VideoBackground
      src="https://cyber-concepts-nyc-assets.s3.amazonaws.com/Cyber-City.mp4"
      style="max-height: 400px; height: 100vh;"
    >
      <TypeWritter 
        class="video-overlay-text" 
        title="We Accelerate " 
        :words="['Startups', 'Companies', 'Products']"
        :speed="300"
        :deleteSpeed="150"  
      />
    </VideoBackground> -->
    <!-- Initial pitch, inspo -->
    <div id="pitches"
      v-for="(item, key) in pitches" 
      :key="key"
      class="sections"
    >
      <Pitch :pitch="item" />
    </div>
    <div id="past-customers">
      <div
        v-for="(item, key) in pastCustomers"
        :key="key"
      >
        <PastClient 
          :logo="item.logo" 
          :name="item.title" 
          :quote="item.content"
          :position="item.position"
          :weblink="item.webLink"
          :background="item.background"
          :impact="item.impact"
        ></PastClient>
      </div>
    </div>
    <!-- signup -->
    <div class="call-to-action">
      <b-img :src="logo"></b-img>
      <!-- <b-row>
        <b-col>
          <router-link to="Services">
            <b-button variant="outline-primary">AVAILABLE OFFERINGS</b-button>
          </router-link>
        </b-col>
      </b-row> -->
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
import NavBar from '../components/NavBar.vue';
import Pitch from '../components/Pitch.vue';
import Footer from '../components/Footer.vue';
import spiraLogo from '../assets/spira-logo.png';
import makecentsLogo from '../assets/MakeCents-logo.jpg';
import agLogo from '../assets/adrianople-dark.png';
import appStackLogo from '../assets/appstack.png';
import levelScapeLogo from '../assets/levelscape-logo.jpg';
import cyanRoom from '../assets/corporate-future.png';
import logo from '../assets/cc_logo_1_wht.svg';
import PastClient from '../components/PastClient2.vue';

export default {
  components: {
    NavBar,
    Pitch,
    Footer,
    PastClient
  },
  data() {
    return {
      scrollPosition: 0,
      isNavBackground: false,
      backgroundClass: '',
      topPosition: 0,
      logo: logo,
      msg: null,
      pitches: [
        {
          champion: "WE TAKE STARTUPS FROM 0 TO 1",
          styleObject: {
            "background": "#010303",
            
          },
          assets: {
            centerImage: "motherboard.jpg",
          }
        },
        {
          champion: "WE PROVIDE APPLIED INNOVATION",
          styleObject: {
            // "background": "linear-gradient(45deg, rgb(204, 228, 240), rgb(182, 190, 218))",
          },
          assets: {
            backgroundImage: cyanRoom,
          }
        },
        {
          champion: "WE SIMPLIFY THE COMPLEX",
          styleObject: {
            "background": "linear-gradient(90deg, rgb(204, 228, 240), rgb(123, 138, 193))"
          },
          assets: {
            centerImage: null,
          }
        }
      ],
      pastCustomers : [
        {
          title: 'Adrianople Group',
          logo: agLogo,
          webLink: 'https://www.adrianoplegroup.com/',
          content: 'Adrianople Group provides world class research and advisory services on Special Economic Zones.',
          img_class: "img-background-light",
          img_container_class: "img-container-light",
          position: 'left',
          background: '#ffffff',
          impact: 'We created an interactive map application displaying thier research expertise'
        },
        {
          title: 'MakeCents',
          logo: makecentsLogo,
          webLink: 'https://www.crunchbase.com/organization/makecents',
          content: 'MakeCents is the payments platform for faccilitating payments too and between businesses.',
          position: 'right',
          background: '#f2f2f2',
          impact: 'We designed, developed and deployed the digital payments solution with our select expertise.'
        },
        {
          title: 'Spira',
          logo: spiraLogo,
          webLink: 'https://www.spirainc.com/',
          content: 'Spira is the provider of the electric sky dye. Spira is the leading biofoundry specialized in alage.',
          position: 'left',
          background: '#ffffff',
          impact: 'We consulted on avante guard strategies to disrupt the biology/biotech industry.'
        },
      ],
      sisterOrgs : [
        {
          title: 'AppStack Inc',
          logo: appStackLogo,
          webLink: 'https://www.appstack.nyc/onboarding',
          content: "You have the vision for a stunning digital experience. We're the software design and engineering team that can bring it to life. A bespoke product development and consignment firm that specializes in developing minimum viable products and scalling, post launch."
        },
        {
          title: 'Levelscape Inc',
          logo: levelScapeLogo,
          webLink: 'https://www.levelscape.net/',
          content: 'Levelscape builds technology to simplify data engineering and automation. Focus on making decisions instead of generating reports. Based in New York City, Levelscape offers solutions to clients of all sizes to succeed in an increasingly complex world.'
        },
      ]
    };
  },
  methods: {
    handleScroll() {
      this.topPosition = window.scrollY;
      this.determineNavBackground();
    },
    determineNavBackground() {
      try {
        let wrappers = document.getElementsByClassName("wrapper");
        let wrapper1 = wrappers[0].getBoundingClientRect().top + window.scrollY;
        let wrapper2 = wrappers[1].getBoundingClientRect().top + window.scrollY;
        let wrapper3 = wrappers[2].getBoundingClientRect().top + window.scrollY;
        if(this.topPosition <= wrapper2) {
          this.backgroundClass = 'motherboard'
          this.isNavBackground = true;
        } else if (this.topPosition > wrapper2 && this.topPosition <= wrapper3) {
          this.backgroundClass = 'neon';
          this.isNavBackground = true;
        } else if (this.topPosition > wrapper3) {
          this.backgroundClass = 'cloud';
          this.isNavBackground = true;
        }
      } catch (err) {
        if(typeof err === 'TypeError') {
          // pass silently
          ;
        }
      }
    },
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll);
  },
  beforeDestroy() {
    window.removeEventListener('scroll', this.handleScroll);
  }
};
</script>

<style lang="scss" scoped>
  $lightGrey: rgb(241, 234, 234);
  $transGray: rgba(241,234,234, 0.25);

  #navbar.motherboard {
    background-color: rgba($color: #000000, $alpha: 0.0);
  }
  #navbar.neon {
    background-color: #ed36c8;
  }
  #navbar.cloud {
    background-color: #000;
  }

  #home {
    color: $lightGrey;
    background-color: #000;
    height: 100%;
    width: 100%;
    #pitches {
      height: 100%;
      .sections {
        height: 100%;
      }
    }
  }

  .videobg-content {
    display: table;

    .video-overlay-text {
      display: table-cell;
      vertical-align: middle;
      text-align: center;
      font-size: 5rem;
      @media screen and (max-width: 750px) {
        font-size: 2.5rem;
      }
    }
  }

  a:hover {
    text-decoration: none !important;
  }

  .btn-primary {
    background-color: #151515 !important;
    border-color: #151515 !important;
    color: $lightGrey !important;
    font-size: 2rem !important;
    font-weight: 700 !important;
    text-decoration: none !important;
  }

  .btn-primary:hover {
    background-color: $lightGrey !important;
    border-color: $lightGrey !important;
    color: #151515 !important;
    text-decoration: none !important;
  }

  .btn-outline-primary {
    background-color: rgba(0,0,0,0) !important;
    border-color: $lightGrey !important;
    color: $lightGrey !important;
    // font-size: 2rem !important;
    // font-weight: 700 !important;
    text-decoration: none !important;
  }

  .btn-outline-primary:hover {
    background-color: $lightGrey !important;
    border-color: $lightGrey !important;
    color: #151515 !important;
    text-decoration: none !important;
  }

  .custom-spacer {
    border-style: solid;
    border-color: $transGray;
    border-width: 1px;
    margin-top: 3rem;
    margin-bottom: 3rem;
  }

  .offerings-container, .clients-container, .partners-container {
    h1 {
      margin-top: 3rem;
      margin-bottom: 3rem;
      font-weight: 800;
    }
  }

  .call-to-action {
    padding-top: 1rem;
    padding-bottom: 1rem;
    background: #000;
    img {
      padding-bottom: 1rem;
      max-width: 300px;
      max-height: 300px;
    }
    .row {
      padding-top: 1rem;
    }
  }

</style>
