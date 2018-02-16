<template>
  <div>
    <svg id="circle"  :width="width" :height="height" style="border: 1px">
    </svg>
  </div>
</template>

<script>
import * as d3 from 'd3v4'

export default {
  name: 'App',
  data () {
    return {
      width: 800,
      height: 500,
      r: 75
    }
  },
  methods: {
  },
  mounted () {
    let svg1 = d3.select('#circle')
    let svg2 = d3.select('#circle')
    let svg3 = d3.select('#circle')

    var handler =
      d3.drag()
        .on('start', d => d3.select('#circle').raise().classed('active', true))
        .on('drag', function (d, i, a) {
          console.log(d)
          d3.select(this).attr('cx', d.x = d3.event.x).attr('cy', d.y = d3.event.y)
        })
        .on('end', d => d3.select('#circle').classed('active', false))

    svg1.append('circle')
      .attr('cx', this.width / 2)
      .attr('cy', this.height / 2)
      .attr('r', this.r)
      .datum({x: this.width / 2, y: this.height / 2})
      .style('fill', 'skyblue')
      .call(handler)

    svg2.append('circle')
      .attr('cx', this.width / 4)
      .attr('cy', this.height / 4)
      .attr('r', this.r / 4)
      .datum({x: this.width / 4, y: this.height / 4})
      .style('fill', 'pink')
      .call(handler)

    var lineHandler =
      d3.drag()
        .on('start', d => d3.select('#circle').raise().classed('active', true))
        .on('drag', function (d, i, a) {
          console.log(d3.event)
          d3.select(this).attr('transform', 'translate(300, 150) rotate(-' + d3.event.x + ')')
        })
        .on('end', d => d3.select('#circle').classed('active', false))

    svg3.append('line')
      .attr('x1', 5)
      .attr('y1', 5)
      .attr('x2', 400)
      .attr('y2', 400)
      .attr('stroke-width', 2)
      .style('stroke', 'green')
      .datum({r: this.r})
      .call(lineHandler)
  }
}
</script>

<style>
</style>
