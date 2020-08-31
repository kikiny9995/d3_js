<template>
  <div>
    <el-row>
      <div class="ga-box" id="m_great">母系曾祖輩</div>
      <div class="ga-box" id="p_great">父系曾祖輩</div>
    </el-row>
    <el-row>
      <div class="ga-box" id="m_grand">母系祖輩</div>
      <div class="ga-box" id="p_grand">父系祖輩</div>
    </el-row>
    <el-row>
      <div class="ga-box" id="m__elder">母系長輩</div>
      <div class="ga-box" id="parents">父母輩</div>
      <div class="ga-box" id="p_elder">父系長輩</div>
    </el-row>
    <!-- <div id="straightline">直線</div>
    <div id="horizontalline">橫線</div> -->
  </div>
</template>

<script>
  //https://juejin.im/post/6844903697600757774
  import * as d3 from "d3";
  export default {
    name: "App",
    data() {
      return {}
    },
    methods: {
      connection() {

        //母系曾祖-祖連接線
        this.connectionCalculation('#m_great', '#m_grand');

        //母系祖-長輩連接線
        this.connectionCalculation('#m_grand', '#m__elder');

        //父系曾祖-祖連接線
        this.connectionCalculation('#p_great', '#p_grand');

        //父系祖-長輩連接線
        this.connectionCalculation('#p_grand', '#p_elder');
      },
      connectionCalculation(startId, endId) {
        const startRect = document.querySelector(startId).getBoundingClientRect();
        const endRect = document.querySelector(endId).getBoundingClientRect();

        var x = startRect.width / 2;
        var startY = startRect.height;
        var endY = endRect.bottom - startRect.bottom;
        var lineData = [
          [x, startY],
          [x, endY]
        ];

        var width = startRect.width;
        var height = endY;
        var svg = d3.select(startId).append("svg")
          .attr("width", width)
          .attr("height", height)
          .attr("class", "position-svg");

        var line = d3.line();

        svg.append("path")
          .attr("d", line(lineData))
          .attr("stroke", "black")
          .attr("stroke-width", "1px")
          .attr("fill", "none");
      },
      //橫線
      horizontalline() {
        var lineData = [
          [100, 50],
          [100, 100]
        ];

        var svg = d3.select("#straightline").append("svg")
          .attr("width", "300")
          .attr("height", "300");

        var line = d3.line();

        svg.append("path")
          .attr("d", line(lineData))
          .attr("stroke", "black")
          .attr("stroke-width", "1px")
          .attr("fill", "none");
      },
      //直線
      straightline() {
        var lineData = [
          [50, 50],
          [100, 50]
        ];

        var svg = d3.select("#straightline").append("svg")
          .attr("width", "300")
          .attr("height", "300");

        var line = d3.line();

        svg.append("path")
          .attr("d", line(lineData))
          .attr("stroke", "black")
          .attr("stroke-width", "1px")
          .attr("fill", "none");
      }
    },
    mounted() {
      this.straightline();
      this.horizontalline();
      this.connection();
    },
  };

</script>
<style>
  .ga-box {
    float: left;
    margin-right: 20px;
    margin-bottom: 50px;
    border: 1px solid;
    position: relative;
    z-index: 999;
    width: 100px;
  }

  .position-svg {
    position: absolute;
    left: 0;
  }

</style>
