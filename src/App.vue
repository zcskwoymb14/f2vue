<script>
import { toRaw } from "vue";
import Canvas from "@antv/f-vue";
import { Chart, Interval, Axis, Line, Legend } from "@antv/f2";

const data1 = [
  { genre: "Sports", sold: 275, soldl: 333 },
  { genre: "Strategy", sold: 115, soldl: 333 },
  { genre: "Action", sold: 120, soldl: 333 },
  { genre: "Shooter", sold: 350, soldl: 333 },
  { genre: "Other", sold: 150, soldl: 333 },
];

const data2 = [
  { genre: "Sports", sold: 275, soldl: 333 },
  { genre: "Strategy", sold: 115, soldl: 333 },
  { genre: "Action", sold: 20, soldl: 333 },
  { genre: "Shooter", sold: 50, soldl: 66 },
  { genre: "Other", sold: 50, soldl: 333 },
];

const pieData = [
  {
    name: "股票类",
    percent: 83.59,
    a: "1",
  },
  {
    name: "债券类",
    percent: 2.17,
    a: "1",
  },
  {
    name: "现金类",
    percent: 14.24,
    a: "1",
  },
];

export default {
  name: "App",
  data() {
    return {
      year: "2021",
      chartData: data1,
      pieData: pieData,
    };
  },
  mounted() {
    setTimeout(() => {
      this.year = "2022";
      this.chartData = data2;
    }, 1000);
  },
  render() {
    const { year, chartData } = this;
    return (
      <div className="container">
        <p>折线</p>
        <Canvas pixelRatio={window.devicePixelRatio}>
          <Chart data={toRaw(chartData)}>
            <Axis field="genre" />
            <Axis max="444" field="sold" />
            <Line x="genre" y="soldl" />
            <Interval x="genre" y="sold" color="genre" />
          </Chart>
        </Canvas>
        <p>条形图</p>
        <Canvas pixelRatio={window.devicePixelRatio}>
          <Chart
            data={toRaw(chartData)}
            coord={{
              transposed: true,
            }}
          >
            <Axis field="genre" />
            <Axis max="444" field="sold" />
            <Interval
              style={{
                field: "tem",
                radius: "20",
              }}
              color="#FCCF5E"
              x="genre"
              y="sold"
            />
          </Chart>
        </Canvas>
        <p>圆环饼图</p>
        <Canvas
          pixelRatio={window.devicePixelRatio}
          theme={{ padding: [20, "auto"] }}
        >
          <Chart
            scale={{
              percent: {
                formatter: function formatter(val) {
                  return val + "%";
                },
              },
            }}
            data={toRaw(pieData)}
            coord={{
              type: "polar",
              transposed: true,
              innerRadius: 0.7,
              radius: 0.85,
            }}
          >
            <Interval
              x="a"
              y="percent"
              adjust="stack"
              color={{
                field: "name",
                range: ["#FE5D4D", "#3BA4FF", "#737DDE"],
              }}
            />
            <Legend
              position="right"
              itemFormatter={(val, name) => {
                console.log("val ", val, " name: ", name);
              }}
            />
          </Chart>
        </Canvas>
      </div>
    );
  },
};
</script>

<style>
.container {
  width: 500px;
  height: 300px;
}
</style>
