<script>
  import Meta from "./Meta.svelte";
  import Title from "./Components/Title.svelte";
  import Intro from "./Components/Intro.svelte";
  import TextAndMathEquations from "./Components/TextAndMathEquations.svelte";
  import LineChart from "./Components/LineChart.svelte";
  import ScrollCenter from "./Components/ScrollCenter.svelte";
  import Conclusion from "./Components/Conclusion.svelte";
  import References from "./Components/Resources.svelte";
  import ScrollonLeftSide from "./Components/ScrollSide.svelte";
  import Scrollonright from "./Components/ScrollSide_on_right_lol.svelte"

  import FirstGen from "./Components/1st_gen.svelte"
  import SecondGen from "./Components/2nd_gen.svelte"
  import ThirdGen from "./Components/3rd_gen.svelte"
  import FourthGen from "./Components/4th_gen.svelte"
  import FifthGen from "./Components/5th_gen.svelte"
  import SixthGen from "./Components/6th_gen.svelte"
  import SeventhGen from "./Components/7th_gen.svelte"
  import EighthGen from "./Components/8th_gen.svelte"
  import NinthGen from "./Components/9th_gen.svelte"
  import Final_chart from "./Components/final_chart.svelte"

  import Nintendo from "./Components/nintendo.svelte";
  import Sony from "./Components/sony.svelte";
  import Microsoft from "./Components/Microsoft.svelte";
  import Sega from "./Components/Sega.svelte";
  import Atari from "./Components/Atari.svelte";
  import Coleco from "./Components/Coleco.svelte";
  import Magnavox from "./Components/Magnavox.svelte";
</script>


<!--
I have checked the code basically each subcode in components conmtrols one part. We don't need textandmathequations and let's first see it scrollside alone works if it is too redundent, we can changechangechang
-->

<Meta /> <!-- The otherall styling of title -->
<Title /> 

<!-- 1st gen , we can have a side scroll on each section-->
<Magnavox />
<Nintendo />
<Atari />


<FirstGen />

<!-- 2nd gen -->

<Coleco />
<SecondGen />

<!-- 3rd gen -->
<ThirdGen />

<!-- 4th gen -->
<FourthGen />

<!-- 5th gen -->
<FifthGen />


<!-- 6th gen -->
<SixthGen />

<!-- 7th gen -->
<SeventhGen />

<!-- 8th gen -->
<EighthGen />

<!-- 9th gen -->
<NinthGen />

<!-- Test -->
<Sony />
<Microsoft />

<Sega />


<!-- <ScrollonLeftSide /> 
<Scrollonright /> <I made this copy, we can use more here and there. -->
<!-- <LineChart /> --> 
<Final_chart />


<!-- <Conclusion /> -->

<References />
