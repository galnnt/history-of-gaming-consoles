<script>
  import { onMount } from 'svelte';
  import Meta from "./Meta.svelte";
  import Title from "./Components/Title.svelte";
  import Intro from "./Components/Intro.svelte";
  import TextAndMathEquations from "./Components/TextAndMathEquations.svelte";
  import LineChart from "./Components/LineChart.svelte";
  import ScrollCenter from "./Components/ScrollCenter.svelte";
  import Conclusion from "./Components/Conclusion.svelte";
  import References from "./Components/Resources.svelte";
  import ScrollonLeftSide from "./Components/ScrollSide.svelte";
  import Scrollonright from "./Components/ScrollSide_on_right_lol.svelte";
  import FirstGen from "./Components/1st_gen.svelte";
  import SecondGen from "./Components/2nd_gen.svelte";
  import ThirdGen from "./Components/3rd_gen.svelte";
  import FourthGen from "./Components/4th_gen.svelte";
  import FifthGen from "./Components/5th_gen.svelte";
  import SixthGen from "./Components/6th_gen.svelte";
  import SeventhGen from "./Components/7th_gen.svelte";
  import EighthGen from "./Components/8th_gen.svelte";
  import NinthGen from "./Components/9th_gen.svelte";
  import Hook from "./Components/hook.svelte"



  import HUD from "./HUD.svelte";
  import { Sidepanel } from 'svelte-mui';
  import {Button, Checkbox } from 'svelte-mui';

  let items = [];
  let rightVisible = false;
  let activeSection = 0;
  
  const sections = [
    "First Generation",
    "Second Generation",
    "Third Generation",
    "Fourth Generation",
    "Fifth Generation",
    "Sixth Generation",
    "Seventh Generation",
    "Eighth Generation",
    "Ninth Generation",
    "Conclusion"
  ];

  function handleIntersection(entries) {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        activeSection = parseInt(entry.target.dataset.index, 10);
      }
    });
  }

  onMount(() => {
    const observer = new IntersectionObserver(handleIntersection, {
      root: null,
      rootMargin: '0px',
      threshold: 0.5
    });

    const elements = document.querySelectorAll('.section');
    elements.forEach((el, index) => {
      el.dataset.index = index;
      observer.observe(el);
    });
  });
</script>
``

<!-- <HUD_button />
<Sidepanel right bind:visible={rightVisible}>
  <div class="logo" style="padding-left: 1rem;">Help</div>
  <p>
    <i style="padding: 12px;">Blank</i>
  </p>
  <HUD {sections} bind:activeSection />
</Sidepanel> -->


<Hook />

<Meta />
<Title />

<!-- Add the HUD component -->
<HUD {sections} bind:activeSection />


<!-- Sections -->
<div id="section-0" class="section"><FirstGen /></div>
<div id="section-1" class="section"><SecondGen /></div>
<div id="section-2" class="section"><ThirdGen /></div>
<div id="section-3" class="section"><FourthGen /></div>
<div id="section-4" class="section"><FifthGen /></div>
<div id="section-5" class="section"><SixthGen /></div>
<div id="section-6" class="section"><SeventhGen /></div>
<div id="section-7" class="section"><EighthGen /></div>
<div id="section-8" class="section"><NinthGen /></div>
<div id="section-9" class="section"><Conclusion /></div>
<References />


<style>
  .section {
    scroll-margin-top: 20px; /* Adjust if necessary to account for fixed header */
  }
</style>
