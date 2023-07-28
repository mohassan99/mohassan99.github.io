layout: page
title: "Four Cylinder Engines"
permalink: /Four_Cylinder

<!DOCTYPE html>
<html lang="en">
<script src='https://d3js.org/d3.v5.min.js'></script>
<style> circle {fill: lightblue; stroke: black;} </style>
<body onload='init()'>
<svg width=300 height=300> </svg>

<script>
    async function init() {
        /* Code Here */
        const data4 = await d3.csv('https://mohassan99.github.io/cars2017_4.csv');

        var y = d3.scaleLog().domain([10, 150]).range([200, 0]);
        var x = d3.scaleLog().domain([10, 150]).range([0, 200]);
        var margin = 50;
        var height = 200;

        d3.select("svg")
            .append("g")
            .attr("transform","translate("+margin+","+(+margin)+")")
            .selectAll("circle")
            .data(data4)
            .enter()
            .append("circle")
            .attr("cx", function(d) {return x(+d.AverageCityMPG); } )
            .attr("cy", function(d) {return y(+d.AverageHighwayMPG); } )
            .attr("r",  function(d) {return 2+ +d.EngineCylinders; } )
        ;

        d3.select("svg")
            .append("g")
            .attr("transform","translate("+margin+","+margin+")")
            .call(d3.axisLeft(y)
                .tickValues([10, 20, 50, 100])
                .tickFormat(d3.format("~s"))
            )
        ;
        d3.select("svg")
            .append("g")
            .attr("transform","translate("+margin+","+(height+margin)+")")
            .call(d3.axisBottom(x)
                .tickValues([10, 20, 50, 100])
                .tickFormat(d3.format("~s"))
            )
        ;
    }
</script>
</body>
</html>