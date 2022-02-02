<template>
  <div class="gauge">
    <div class="gauge">
      <GChart
        type="Gauge"
        :data="kwh"
        :options="options"
        :settings="{ packages: ['corechart', 'gauge'] }"
      />
    </div>
  </div>
</template>

<script>
import WebSocket from "isomorphic-ws";
import { GChart } from "vue-google-charts";
export default {
  data() {
    return {
      kwh: [
        ["Label", "Value"],
        ["KWH", 5],
      ],
      options: {
        width: 400,
        height: 600,
        max: 10,
        redFrom: 7,
        redTo: 10,
        yellowFrom: 1,
        yellowTo: 7,
        greenFrom: 0,
        greenTo: 1,
        minorTicks: 5,
      },
    };
  },
  components: {
    GChart,
  },
  methods: {
    onChartReady(chart, google) {
      console.log(google);
      chart.draw(this.kwh, this.options);
    },
  },
  mounted() {
    const ws = new WebSocket("wss://power-monitor-ws.soxprox.com");
    ws.onopen = function open() {
      console.log("connected");
    };
    ws.onmessage = (data) => {
      this.kwh = [
        ["Label", "Value"],
        ["KWH", parseFloat(data.data)],
      ]
    };
  },
};
</script>

<style>

</style>
