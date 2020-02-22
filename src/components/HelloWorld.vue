<template>
  <div class="hello">
    <div ref="checkbox" style="width:900px;height:900px;margin:0 auto;">

    </div>
  </div>
</template>

<script>
import echarts from 'echarts'
import 'echarts/map/js/china'
import jsonp from 'jsonp'
        var option = {
            title: {
                text: 'ECharts 入门示例',
                subtext:"疫情情况报表",
                textStyle:{
                  color:'#cc3113'
                  },
                subtextStyle:{
                  color:'#cc3333',
                  fontStyle:"italic"
                }
            },
                toolbox: {
        feature: {
            saveAsImage: {}
        }
    },
                  tooltip:{
                trigger:'item'
              },
            series:[{
              name:'111111',
              tooltip:{
                 trigger:'item',
                  componentType: 'series',
    // 系列类型
    seriesType: 'string',
    // 系列在传入的 option.series 中的 index
    seriesIndex: 'number',
    // 系列名称
    seriesName: 'string',
    // 数据名，类目名
    name: 'string'
              },
               data:[],
              type : 'map',
              map:'china',
              roam:true,
              zoom:1.2,
              label:{
                show:true,
              },
              itemStyle:{
                areaColor : '#aa3333',
                borderColor:'aa1111'
              },
               emphasis:{
                 label:{
                   show:true,
                   color:'#cc1111'
                 },
                 itemStyle:{
                    areaColor :'#eee'
                 }
               }
              
            }],
            visualMap: [{ 
            type: 'piecewise',
            show:true,
            pieces:[
              {min:10000},
               {min:1000,max:9999},
               {min:100,max:999},
               {min:10,max:99},
               {min:1,max:9}
            ],
            itemWidth:30,
            itemHeight :30,
             inRange:{
               symbol:'circle',
               color:['blue','red']
             }
            // align:'right'
            
        }
    ]
   


        };
export default {
mounted(){
  this.myChart = echarts.init(this.$refs.checkbox)
  this.myChart.setOption(option);
  this.getData()
},
methods:{
  getData(){
    jsonp('https://gwpre.sina.cn/interface/fymap2020_data.json',{},(err,data)=>{
      if(!err){
        let lists = data.data.list.map(item=>{
          return {
            name:item.name,
            value:item.value
          }
        })
        option.series[0].data = lists
        console.log(lists)
        this.myChart.setOption(option);
      }else{
        console.log(err)
      }
    })
  }
}
}
</script>


<style scoped>

</style>
