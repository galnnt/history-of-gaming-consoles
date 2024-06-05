<script>
  import { onMount } from "svelte";
  import { scaleOrdinal } from "d3-scale";
  import { arc, pie } from "d3-shape";
  import { select } from "d3-selection";

  let data = [
    { company: "Nintendo", value: 0, console: "" },
    { company: "Sony", value: 0, console: "" },
    { company: "Microsoft", value: 0, console: "" },
    { company: "Sega", value: 0, console: "" },
    { company: "Atari", value: 0, console: "" },
    { company: "Coleco", value: 0, console: "" },
    { company: "Magnavox", value: 0, console: "" },
    { company: "Mattel", value: 0, console: "" },
    { company: "Philips", value: 0, console: "" },
    { company: "NEC", value: 0, console: "" },
    { company: "Bandai", value: 0, console: "" },
    { company: "Nokia", value: 0, console: "" },
  ];

  let generation = 1;

  const salesData = {
    1: [
      { company: "Nintendo", value: 3.00, console: "Color TV-Game" },
      { company: "Coleco", value: 1.00, console: "Telstar" },
      { company: "Magnavox", value: 0.33, console: "Odyssey" }
    ],
    2: [
      { company: "Atari", value: 8.00, console: "Atari 2600" },
      { company: "Coleco", value: 1.00, console: "Telstar" },
      { company: "Mattel", value: 1.00, console: "Intellivision" },
      { company: "Nintendo", value: 1.10, console: "Game & Watch" }
    ],
    3: [
      { company: "Atari", value: 1.00, console: "Atari 7800" },
      { company: "Sega", value: 2.10, console: "Master System" },
      { company: "Nintendo", value: 84.06, console: "NES" }
    ],
    4: [
      { company: "Sega", value: 15.74, console: "Genesis" },
      { company: "Philips", value: 2.00, console: "CD-i" },
      { company: "Nintendo", value: 26.10, console: "SNES" },
      { company: "Atari", value: 0.50, console: "Lynx" },
      { company: "NEC", value: 1.50, console: "TurboGrafx-16" }
    ],
    5: [
      { company: "Nintendo", value: 34.99, console: "N64" },
      { company: "Sony", value: 10.85, console: "PlayStation" },
      { company: "Sega", value: 1.65, console: "Saturn" }
    ],
    6: [
      { company: "Bandai", value: 1.50, console: "WonderSwan" },
      { company: "Sega", value: 2.50, console: "Dreamcast" },
      { company: "Nokia", value: 1.00, console: "N-Gage" },
      { company: "Sony", value: 24.93, console: "PlayStation 2" },
      { company: "Nintendo", value: 23.31, console: "GameCube" },
      { company: "Microsoft", value: 8.50, console: "Xbox" }
    ],
    7: [
      { company: "Nintendo", value: 128.34, console: "Wii" },
      { company: "Sony", value: 21.30, console: "PlayStation 3" },
      { company: "Microsoft", value: 24.00, console: "Xbox 360" }
    ],
    8: [
      { company: "Nintendo", value: 60.45, console: "Wii U" },
      { company: "Microsoft", value: 14.00, console: "Xbox One" },
      { company: "Sony", value: 21.50, console: "PlayStation 4" }
    ],
    9: [
      { company: "Sony", value: 6.50, console: "PlayStation 5" },
      { company: "Microsoft", value: 3.73, console: "Xbox Series X" }
    ]
  };

  const width = 500;
  const height = 500;
  const radius = Math.min(width, height) / 2;

  const color = scaleOrdinal()
    .domain(data.map(d => d.company))
    .range([
      "#FF5733",  // Vibrant Red for Nintendo
      "#1E90FF",  // Vibrant Blue for Sony
      "#32CD32",  // Vibrant Green for Microsoft
      "#FF1493",  // Deep Pink for Sega
      "#FF8C00",  // Dark Orange for Atari
      "#8B4513",  // Saddle Brown for Coleco
      "#808080",  // Gray for Magnavox
      "#FF69B4",  // Hot Pink for Mattel
      "#9400D3",  // Dark Violet for Philips
      "#00FFFF",  // Aqua for NEC
      "#FFD700",  // Gold for Bandai
      "#B22222"   // Firebrick for Nokia
    ]);

  const pieGenerator = pie().value(d => d.value);
  const arcGenerator = arc().innerRadius(0).outerRadius(radius);

  const updateData = (generation) => {
    data = salesData[generation];
    updateChart();
  };

  const updateChart = () => {
    const svg = select("#pie-chart");

    // Remove previous chart elements
    svg.selectAll("*").remove();

    const chartGroup = svg
      .attr("width", width)
      .attr("height", height)
      .append("g")
      .attr("transform", `translate(${width / 2}, ${height / 2})`);

    const totalSales = data.reduce((sum, d) => sum + d.value, 0);

    const paths = chartGroup
      .selectAll("path")
      .data(pieGenerator(data))
      .enter()
      .append("path")
      .attr("d", arcGenerator)
      .attr("fill", d => color(d.data.company))
      .on("mouseover", (event, d) => {
        const tooltip = select("#tooltip");
        tooltip.html(`${d.data.company}<br>Console: ${d.data.console}<br>Sales: ${d.data.value}M`)
          .style("left", `${event.pageX + 10}px`)
          .style("top", `${event.pageY + 10}px`)
          .style("opacity", 1);
      })
      .on("mouseout", () => {
        select("#tooltip").style("opacity", 0);
      });

    chartGroup
      .selectAll("text")
      .data(pieGenerator(data))
      .enter()
      .append("text")
      .attr("transform", d => `translate(${arcGenerator.centroid(d)})`)
      .attr("dy", "0.35em")
      .style("text-anchor", "middle")
      .style("fill", "white")
      .text(d => (d.data.value / totalSales >= 1 / 8) ? d.data.company : "");
  };

  onMount(() => {
    updateData(generation);
  });

  $: updateData(generation);
</script>



<div id="chart-container">
  <div class="slider-container">
    <label for="generation-slider">Generation: {generation}</label>
    <input id="generation-slider" type="range" min="1" max="9" bind:value={generation} />
  </div>
  <svg id="pie-chart"></svg>
  <div id="tooltip" style="position: absolute; opacity: 0; background: #fff; padding: 5px; border: 1px solid #ccc; border-radius: 5px; pointer-events: none;"></div>
</div>

<style>
  @media screen and (max-width: 950px) {
    #intro-hed {
      font-size: 2.5rem;
    }

    .intro-sub {
      font-size: 1.4rem;
    }

    .intro-description {
      font-size: 1rem;
    }
  }

  #chart-container {
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 2rem auto;
    padding: 2rem;
    background-color: #f5f5f5;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }

  .slider-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-bottom: 1rem;
  }

  input[type="range"] {
    width: 100%;
    max-width: 500px;
  }

  svg {
    max-width: 100%;
    height: auto;
  }

  #tooltip {
    position: absolute;
    opacity: 0;
    background: #fff;
    padding: 5px;
    border: 1px solid #ccc;
    border-radius: 5px;
    pointer-events: none;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    font-size: 0.9rem;
    color: #333;
  }
</style>

