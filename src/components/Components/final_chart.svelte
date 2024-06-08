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
    if (typeof document !== 'undefined') {
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
    }
  };

  onMount(() => {
    updateData(generation);
  });

  $: updateData(generation);
</script>

<div id="chart-container">
  <h2 class="chart-title">Market Share for Each Generation</h2>
  <div class="slider-container">
    <label for="generation-slider">Generation: {generation}</label>
    <input id="generation-slider" type="range" min="1" max="9" bind:value={generation} />
  </div>
  <svg id="pie-chart"></svg>
  <div id="tooltip"></div>
  <div class="legend">
    {#each data as { company, value, console }}
      <div class="legend-item">
        <div class="legend-color" style="background-color: {color(company)};"></div>
        <div class="legend-text">{company}</div>
      </div>
    {/each}
  </div>
</div>

<style>
  #chart-container {
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 2rem auto;
    padding: 2rem;
    background-color: transparent; /* Make background transparent */
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    transform: translateY(-20px); /* Move the entire container up by 20px */
  }

  .chart-title {
    font-size: 1.5rem;
    margin-bottom: 1rem;
    text-align: center;
    transform: translateY(-20px); /* Move the title up by 20px */
  }

  .slider-container {
    display: flex;
    align-items: center;
    margin-bottom: 1rem;
    transform: translateY(-20px); /* Move the slider up by 20px */
  }

  .slider-container label {
    margin-right: 1rem;
  }

  #generation-slider {
    width: 200px;
  }

  #pie-chart {
    width: 100%;
    height: 500px;
    transform: translateY(-20px); /* Move the pie chart up by 20px */
  }

  #tooltip {
    position: absolute;
    pointer-events: none;
    background-color: rgba(0, 0, 0, 0.75);
    color: white;
    padding: 0.5rem;
    border-radius: 5px;
    opacity: 0;
    transition: opacity 0.2s;
  }

  .legend {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    margin-top: 1rem;
    transform: translateY(-20px); /* Move the legend up by 20px */
  }

  .legend-item {
    display: flex;
    align-items: center;
    margin: 0.5rem;
  }

  .legend-color {
    width: 20px;
    height: 20px;
    border-radius: 50%;
    margin-right: 0.5rem;
  }

  .legend-text {
    font-size: 0.9rem;
  }
</style>
