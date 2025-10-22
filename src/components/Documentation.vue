<script setup>
import { ref } from "vue";
import Container from "./Container.vue";
import Col from "./Col.vue";
import Row from "./Row.vue";
import Grid from "./Grid.vue";
import Input from "./Input.vue";
import OverlayCard from "./OverlayCard.vue";
import Carousel from "./Carousel.vue";
import CarouselItem from "./CarouselItem.vue";
import Modal from "./Modal.vue";
import FileUploader from "./FileUploader.vue";
import Sidebar from "./Sidebar.vue";
import Table from "@/components/Table.vue";
import Image from "./Image.vue";

const options = [
  {
    value: "test_0",
    name: "Test 0"
  },
  {
    value: "test_1",
    name: "Test 1"
  }
]

const items = [
  {
    group: "Group",
    icon: "file",
    url: "https://digitalpower.ar",
    items: [
      {
        label: "Item 0",
        url: "/",
        icon: "star"
      },
    ],
  },
  {
    label: "Item 1",
    url: "/",
    icon: "star",
    fill: "dodgerblue"
  },
]
const headers = [
  'ID',
  'Name'
];

const data = [
  { id: '1', name: { html: '<p class="m-0">Mike Towers</p>' } },
  { id: '2', name: 'Luis Fonsi' },
  { id: '3', name: 'Karol G' },
  { id: '4', name: 'Bad Bunny' },
  { id: '5', name: 'Sebastián Yatra' },
  { id: '6', name: 'Rosalía' },
  { id: '7', name: 'Ozuna' },
  { id: '8', name: 'J Balvin' },
  { id: '9', name: 'Anuel AA' },
  { id: '10', name: 'Rauw Alejandro' }
];


const htmlPlayground = ref("<h1 slide underline shadow class='m-0 p-3'>Test custom attributes with html below</h1>");
const modal = ref(false);
const Action = (msg = "Button Test") => {
  alert(msg);
}
</script>

<template>
  <Container fade title="Digital Power UI Documentation">
    <div bound class="p-3" nopointer noselect radius-border>
      <b>Atencion</b>
      <br>
      <i>
        <small>
          La siguiente documentacion es valida unicamente para el framework Vue JS 3.x.
          <br>
          Me encuentro trabajando en una futura actualizacion donde esta sea compatible con todos los frameworks y
          librerias
          <br>
          mediante un CDN.
        </small>
      </i>
    </div>
    <br>
    <h2 underline>Index</h2>
    <ul>
      <li><a href="#input">Input</a></li>
      <li class="mt-1"><a href="#grid">Grid</a></li>
      <li class="mt-1"><a href="#carousel">Carousel</a></li>
      <li class="mt-1"><a href="#modal">Modal</a></li>
      <li class="mt-1"><a href="#upload">File Selector</a></li>
      <li class="mt-1"><a href="#sidebar">Sidebar Component</a></li>
      <li class="mt-1"><a href="#overlayCard">Overlay Card</a></li>
      <li class="mt-1"><a href="#table">Table</a></li>
      <li class="mt-1"><a href="#image">Image</a></li>
      <li class="mt-1"><a href="#custom">Custom attributes</a></li>
      <li class="mt-1"><a href="#playground">Playground</a></li>
    </ul>
    <br>

    <h2 underline>Requirements</h2>
    <ul>
      <li>Vue 3</li>
      <li>Box Icons</li>
      <li>Sass</li>
      <li>Sass-loader</li>
      <li>Bootstrap</li>
    </ul>
    <code class="mb-3">npm i boxicons sass sass-loader bootstrap digitalpower</code>
    <br>
    <b>Digital Power CDN</b>
    <code class="mt-2 mb-3">
      &lt;link rel="stylesheet" href="https://digitalpower.ar/cdn/digitalpower.css">
    </code>

    <b>main.js</b>
    <code class="mt-2">
      import { createApp } from 'vue' <br/>
      import './style.css' <br/>
      import App from './App.vue' <br/>
      import { router } from './pages' <br/>
           <br/>
      import './styles.scss' <br/>
      import * as bootstrap from 'bootstrap' <br/>
      import 'boxicons' <br/>
           <br/>
      createApp(App).use(router).mount('#app') <br/>
    </code>

    <br>
    <h2 underline id="input">Input</h2>
    <code class="mt-2">
      &lt;script setup&gt; <br>
        import {Input} from 'digitalpower'; <br>
        const bindValue = ref(''); <br>
        const value = "Text Input"; <br>
        const Placeholder = "Text placeholder"; <br>
        const Label = "Input Label"; <br>
        <br>
        const options = [
          {
            value: "test_0",
            name: "Test 0"
          },
          {
            value: "test_1",
            name: "Test 1"
          }
        ]
      &lt;/script&gt; <br>

      <br>

      &lt;template&gt; <br>
      &lt;Input v-model="bindValue" label="Label" placeholder="Placeholder" value="value" color="red" background="white" /&gt; <br>

      &lt;Input type="button" label="Label" value="value" color="white" background="var(--primary)" @action="alert('Button Test')" /&gt; <br>
      
      &lt;Input type="select" v-model="bindValue" :options="options" label="Label" value="value" /&gt; <br>
      &lt;Input type="select_checkbox" v-model="bindValue" label="Label" value="value" /&gt; <br>
      &lt;Input type="textarea" v-model="bindValue" label="Label" value="value" /&gt; <br>
      &lt;/template&gt; <br>
      <br>

      <Input label="Input Label" placeholder="Text Placeholder" value="Text Input" color="black" background="white" />
      <Input class="mt-2" type="button" value="Button Input" color="white" background="var(--primary)" @action="Action('Button Test')" />
      <Input class="mt-3" type="select" label="Select" :options/>
      <Input class="mt-3" type="select_checkbox" label="Select_checkbox"/>
      <Input class="mt-3" type="textarea" label="Textarea"/>
    </code>
    <br>
    <h2 underline id="grid">Grid System</h2>
    <i><small>Working on Bootstrap (Col & Row)</small></i>
    <code class="mt-2">
      &lt;script setup&gt; <br>
        import {Grid, Row, Col} from 'digitalpower'; <br>
      &lt;/script&gt; <br>
      <br>
      &lt;template&gt; <br>

      &lt;Container&gt; maxWidth="1280px" title="Grid System"&gt; <br>

      &lt;Row&gt; <br>
      &lt;Col xl="6" lg="6" md="12" sm="12" xs="12"&gt; <br>
      &lt;b&gt;Grid example&lt;/b&gt;
      <br>
      &lt;/Col&gt; <br>
      &lt;/Row&gt; <br>
      <br>
      &lt;Grid width="128" gapped radius-border&gt; <br>
      &lt;img v-for="img in 10" width="128px" src="https://wallpaperaccess.com/full/4868335.jpg"&gt;
      &lt;/img&gt; <br>
      &lt;/Grid&gt; <br>
      &lt;/Container&gt; <br>
      &lt;/template&gt; <br>
      <br>
      <Container title="Container Example">
        <Row class="mb-3">
        <Col xl="6" lg="6" md="12" sm="12" xs="12">
          <b>Grid example</b>
        </Col>
      </Row>
      <Grid class="gridd" width="128" gapped radius-border>
        <img v-for="img in 10" width="128px" src="/DigitalPower.png" alt="">
      </Grid>
      </Container>
    </code>
    <br>
    <h2 underline id="Carousel">Carousel System</h2>
    <i><small>Working on Bootstrap</small></i>
    <code>
      &lt;Carousel id="carousel" interval="3000" blackArrows="true"&gt; <br>
      &lt;CarouselItem v-for="(img, key) in 10" :active="key === 0"&gt; <br>
        &lt;div flex-center&gt; <br>
          &lt;img width="128px" src="/DigitalPower.png" alt=""&gt; <br>
        &lt;/div&gt; <br>
      &lt;/CarouselItem&gt; <br>
    &lt;/Carousel&gt;
    </code>

    <Carousel id="carousel" interval="3000" blackArrows="true">
      <CarouselItem v-for="(img, key) in 10" :active="key === 0">
        <div class="carimg" flex-center>
          <img width="128px" src="/DigitalPower.png" alt="">
        </div>
      </CarouselItem>
    </Carousel>
    <br>
    <h2 underline id="modal">Modal System</h2>
    <code>

      &lt;Modal v-if="modal" title="Modal for testing" @close="() => { modal = false; }"&gt; <br>
        &lt;Input type="button" value="Close" @click="() => { emit('close') }" /&gt; <br>
      &lt;/Modal&gt; <br>
      &lt;Input type="button" value="Open" @click="() => { modal = true; }" /&gt; <br>
    </code>
    <br>
    <Modal v-if="modal" title="Modal for testing" @close="() => { modal = false; }">
      <p>You can also click outside for close this modal</p>
      <Input type="button" value="Close" @click="() => { modal = false; }" />
    </Modal>
    <Input type="button" value="Open" @click="() => { modal = true; }" />
    <br>
    <h2 underline id="upload">File Upload</h2>
    <code>
      &lt;FileUploader @action="Action(`Files uploaded: ${$event}`)"&gt;&lt;/FileUploader&gt;
    </code>
    <FileUploader @action="Action(`Files uploaded: ${$event}`)"></FileUploader>
    <br>
    <h2 underline id="sidebar">Sidebar</h2>
    <code>
      const items = [ <br>
      { <br>
        group: "Group", <br>
        icon: "file",<br>
        url: "https://digitalpower.ar",<br>
        items: [
          {
            label: "Item 0",
            url: "/",
            icon: "star"
          },
        ],
      }, <br>
      {
        label: "Item 1",
        url: "/",
        icon: "star",
        fill: "yellow"
      },<br>
    ]<br>
      &lt;Sidebar id="sidebarTest" :items background="white" bordered fixed&gt;&lt;/Sidebar&gt;
    </code>
    <br>
    <div class="sidebarD">
      <Sidebar id="sidebarTest" :items background="white" bordered></Sidebar>
    </div>

    <br>
    <h1 id="overlayCard" underline>Overlay Card</h1>
    <code>
     import {OverlayCard} from 'digitalpower'; <br>
      &lt;OverlayCard :text="'Overlay Card'" :img="digitalpower/logo.png"&gt;&lt;/OverlayCard&gt;
    </code>
    <br>
    <div>
      <OverlayCard img="/DigitalPower.png" text="Overlay Card"></OverlayCard>
    </div>
    <br>

    <br>
    <h1 id="overlayCard" underline>Table</h1>
    <code id="table">
      import {Table} from 'digitalpower'; <br>
      <br>const headers = [
      <br>'ID',
      <br>'Name'
      <br>];

      <br> const data = [
      <br> { id: '1', name: {html: '&lt;p class="m-0">Mike Towers&lt;/p>'} },
      <br> { id: '2', name: 'Luis Fonsi' },
      <br> { id: '3', name: 'Karol G' },
      <br> { id: '4', name: 'Bad Bunny' },
      <br> { id: '5', name: 'Sebastián Yatra' },
      <br> { id: '6', name: 'Rosalía' },
      <br> { id: '7', name: 'Ozuna' },
      <br> { id: '8', name: 'J Balvin' },
      <br> { id: '9', name: 'Anuel AA' },
      <br> { id: '10', name: 'Rauw Alejandro' }
      <br>
      <br>
      // Length defines char limit for field content
      <br> &lt;Table :headers :data length="30" @rightClick="(arg) => {}" @action="(arg) => {}">&lt;/Table>

      ];
    </code>
    <br>
    <div>
      <Table :headers :data length="30"></Table>
    </div>
    <br>

    <br>
    <h1 id="image" underline>Image</h1>
    <code id="table">
      import {Image} from 'digitalpower'; <br>
   
      <br> &lt;Image src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ-vbE6O27KMekexBLwX6LRSiKb75pN9lPiTQ&s" 
      <br>
      width="500px" 
      <br>
      height="256px" 
      <br>
      @error="($evt) => {}" 
      <br>
      @load="($evt) => {}">&lt;/Image>
    </code>
    <br>
    <div>
      <Image src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ-vbE6O27KMekexBLwX6LRSiKb75pN9lPiTQ&s"
        width="500px" height="256px" />
    </div>
    <br>

    <h2 class="mt-4" underline id="custom">Custom attributes</h2>
    <small>Listed below the available custom attributes</small>

    <pre>
      <code>
[flex]                  // Ads display flex
[nopointer]             // Makes element non interactive
[subitem]               // Submenu item style
[groupitem][grouplabel] // Group parent style for sidebar
[menuitem]              // Sidebar item Style
[shadow]                // Adds shadow to element
[borderbottom]          // Adds bottom border (replaced by underline)
[bordered]              // Adds border to element
[radius-border]         // Adds border radius to element
[bound]                 // Ads gradient animation to element
[custominput]           // Custom input style
[customselect]          // Custom select style
[flex-center]           // Ads flex and centers element childs
[flex-start]            // Ads flex and starts element childs
[flex-column]           // Ads flex with column direction
[block-center]          // Ads block and centers
[overlay]               // Overlay styles
[inside-verlay]         // Overlay styles
[fade]                  // Adds fade effect
[delayedfade]           // Adds fade effect with programatic delay
[absolute-centered]     // Ads position absolute and centers
[list]                  // Ads list style
[gapped]                // Adds gap to element
[noselect]              // Makes element non selectable
[underline]             // Adds animated underline
[nowrap]                // Adds no wrap to element
[pointer]               // Adds pointer to element
[select]                // Select style

// Slide effects
[slide][slideRight][slideUp][slideDown] 
[fixed]
      </code>
    </pre>
    <br>
    <h2 underline id="playground">Playground</h2>
    <pre v-html="htmlPlayground" class="p-3 mb-3" bordered radius-border></pre>
    <Input type="textarea" v-model="htmlPlayground" :value="htmlPlayground" />
  </Container>
</template>

<style>
code {
  padding: 1em;
  display: block;
  background: rgb(238, 238, 238);
  color: black !important;
}

pre {
  background: transparent;
}

a {
  text-decoration: none !important;
}

#carousel {
  height: 200px;
}

.carimg {
  height: 100%;
}

.gridd {
  background: var(--primary);
  padding: 1em;
}

.sidebarD {
  height: 300px;
}
</style>
