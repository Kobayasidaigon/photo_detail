
<script>
import { Radar } from "vue-chartjs";
export default {
  name:'Chart',
  extends: Radar,
  mounted() {
    this.renderChart(
      {
        labels: ["Red", "Blue", "Yellow", "Green", "Purple", "Orange"],
        datasets: [
          {
            label: "# of Votes",
            data: [12, 0, 3, 4, 2, 3],
            backgroundColor: [
              "rgba(255, 99, 132, 0.2)",
              "rgba(54, 162, 235, 0.2)",
              "rgba(255, 206, 86, 0.2)",
              "rgba(75, 192, 192, 0.2)",
              "rgba(153, 102, 255, 0.2)",
              "rgba(255, 159, 64, 0.2)"
            ],
            borderColor: [
              "rgba(255, 99, 132, 1)",
              "rgba(54, 162, 235, 1)",
              "rgba(255, 206, 86, 1)",
              "rgba(75, 192, 192, 1)",
              "rgba(153, 102, 255, 1)",
              "rgba(255, 159, 64, 1)"
            ],
            borderWidth: 0
          }
        ]
      },
      { responsive: true, maintainAspectRatio: false }
    );
    this.check();
  },
  props:["label"], // シンプルシンタックス
  methods:{
    check:function () {
    console.log(this.label);
  }

  } 
};
</script>