
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
      this.draw_graph();
      //次回以降の表示のために削除
      this.safe_point=[];
    },
    change_string_to_number:function(string){
        if(string==="VERY_UNLIKELY"){
          this.safe_point.push("2");
        }
        else if(string==="UNLIKELY"){        
          this.safe_point.push("4");
        }
        else if(string==="POSSIBLE"){    
          this.safe_point.push("6");
        }
        else if(string==="LIKELY"){    
          this.safe_point.push("8");
        }
        else if(string==="VERY_LIKELY"){   
          this.safe_point.push("10");
        }
    },
    draw_graph:function(){
      
    this.renderChart(
      {
        labels: ["アダルト", "なりすまし", "医療", "暴力的", "際どい表現"],
        datasets: [
          {
            label: "成分",
            data: this.safe_point,
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
            borderWidth: 2
          }
        ]
      },
      { responsive: true, maintainAspectRatio: false }
    );
    }
  } 
};
</script>