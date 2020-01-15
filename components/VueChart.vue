
<script>
import { Radar } from "vue-chartjs";
export default {
  data:function(){{
    return{
      safe_data:[],
      safe_point:[]
    }
  }},
  name:'Chart',
  extends: Radar,
  mounted() {
    this.renderChart(
      {
        labels: ["adult", "spoof", "medical", "violence", "racy"],
        datasets: [
          {
            label: "成分",
            data: [12, 3, 4, 2, 3],
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
  props:["safe"], 
  methods:{
    check:function () {
      this.safe_data = this.safe;
      this.change_string_to_number(this.safe_data[0].adult);
      this.change_string_to_number(this.safe_data[0].spoof);
      this.change_string_to_number(this.safe_data[0].medical);
      this.change_string_to_number(this.safe_data[0].violence);
      this.change_string_to_number(this.safe_data[0].racy);
    },
    change_string_to_number:function(string){
        if(string==="VERY_UNLIKELY"){
          this.safe_point.push("0");
        }
        if(string==="UNLIKELY"){        
          this.safe_point.push("1");
        }
        if(string==="LIKELY"){    
          this.safe_point.push("2");
        }
        if(string==="VERY_LIKELY"){   
          this.safe_point.push("3");
        }
    }
  } 
};
</script>