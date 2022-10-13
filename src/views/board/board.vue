<template>
    <div class="flex flex-wrap items-left">
        <el-form-item label="选择客户端服务器" prop="">
            <el-select v-model="hostname" placeholder="" @change="selectChange">
                <el-option
                    v-for="item in tableData"
                    :key="item.id"
                    :label="item.content"
                    :value="item.ip"
                />
            </el-select>
        </el-form-item>

        <div class="aaaa">
            <div id="echartsInfoOne" :style="{ width: '100%', height: '500px' }"></div>
            <div id="echartsInfoOne2" :style="{ width: '100%', height: '500px' }"></div>
            <div id="echartsInfoOne3" :style="{ width: '100%', height: '500px' }"></div>
        </div>
    </div>
</template>

<script setup>
import { ArrowDown } from '@element-plus/icons-vue'
import { ref,onUnmounted } from 'vue';
import * as echart from 'echarts';
import { allMachine, clientSysCpu, clientSysMen, clientSysDisk } from '@/request/api';

const tableData = ref([]);
const hostname = ref("")
const all_machine = async () => {
    let res = await allMachine()
    if (res.code !== 2000) {
        res.data = []
    }
    tableData.value = res.data
    hostname.value = res.data[0].ip
    getOrderCount()
    getMemPercent()
    getDiskPercent()
}
all_machine()
    const selectChange = (e) => {
        hostname.value = e
        getOrderCount()
        getMemPercent()
        getDiskPercent()
    }
    const data1 = ref([])
    const data2 = ref([])
    const data3 = ref([])
    const channel1 = ref("")
    const channel2 = ref("")
    const channel3 = ref("")
    const num = ref(0)
    const num2 = ref(0)
    const num3 = ref(0)
    const getOrderCount = async () => {
        clearTimeout(channel1.value)
        channel1.value = setTimeout(()=>{
            getOrderCount()
            let echartsInfoOne = document.getElementById("echartsInfoOne")
            let chart = echart.init(echartsInfoOne);
            if(60 < data1.value.length) {
                data1.value.shift()
            }
            chart.setOption({
                series: [
                    {
                        data: [data1.value[0],data1.value[1],data1.value[2],data1.value[3],data1.value[4],data1.value[5],data1.value[6],data1.value[7],data1.value[8],data1.value[9],
                        data1.value[10],data1.value[11],data1.value[12],data1.value[13],data1.value[14],data1.value[15],data1.value[16],data1.value[17],data1.value[18],data1.value[19],
                        data1.value[20],data1.value[21],data1.value[22],data1.value[23],data1.value[24],data1.value[25],data1.value[26],data1.value[27],data1.value[28],data1.value[29],
                        data1.value[30],data1.value[31],data1.value[32],data1.value[33],data1.value[34],data1.value[35],data1.value[36],data1.value[37],data1.value[38],data1.value[39],
                        data1.value[40],data1.value[41],data1.value[42],data1.value[43],data1.value[44],data1.value[45],data1.value[46],data1.value[47],data1.value[48],data1.value[49],
                        data1.value[50],data1.value[51],data1.value[52],data1.value[53],data1.value[54],data1.value[55],data1.value[56],data1.value[57],data1.value[58],data1.value[59],
                        data1.value[60],data1.value[61],data1.value[62],data1.value[63],data1.value[64],data1.value[65],data1.value[66],data1.value[67],data1.value[68],data1.value[69],
                        data1.value[70],data1.value[71],data1.value[72],data1.value[73],data1.value[74],data1.value[75],data1.value[76],data1.value[77],data1.value[78],data1.value[79],
                        data1.value[80],data1.value[81],data1.value[82],data1.value[83],data1.value[84],data1.value[85],data1.value[86],data1.value[87],data1.value[88],data1.value[89],
                        data1.value[90],data1.value[91],data1.value[92],data1.value[93],data1.value[94],data1.value[95],data1.value[96],data1.value[97],data1.value[98],data1.value[99],
                        data1.value[100],data1.value[101],data1.value[102],data1.value[103],data1.value[104],data1.value[105],data1.value[106],data1.value[107],data1.value[108],data1.value[109],
                        data1.value[110],data1.value[111],data1.value[112],data1.value[113],data1.value[114],data1.value[115],data1.value[116],data1.value[117],data1.value[118],data1.value[119]]
                    }
                ]
            });
            num.value++
        },30000)
        const res = await clientSysCpu({
            ip: hostname.value
        })
        if(res){
            data1.value = res.data

            if(num.value == 0){
                initEcharts()
            }
        }
    }

    const getMemPercent = async () => {
        clearTimeout(channel2.value)
        channel2.value = setTimeout(()=>{
            getMemPercent()
            let echartsInfoOne2 = document.getElementById("echartsInfoOne2")
            let chart2 = echart.init(echartsInfoOne2);

            if(60 < data2.value.length) {
                data2.value.shift()
            }
            chart2.setOption({
                series: [
                    {
                        data: [data2.value[0],data2.value[1],data2.value[2],data2.value[3],data2.value[4],data2.value[5],data2.value[6],data2.value[7],data2.value[8],data2.value[9],
                            data2.value[10],data2.value[11],data2.value[12],data2.value[13],data2.value[14],data2.value[15],data2.value[16],data2.value[17],data2.value[18],data2.value[19],
                            data2.value[20],data2.value[21],data2.value[22],data2.value[23],data2.value[24],data2.value[25],data2.value[26],data2.value[27],data2.value[28],data2.value[29],
                            data2.value[30],data2.value[31],data2.value[32],data2.value[33],data2.value[34],data2.value[35],data2.value[36],data2.value[37],data2.value[38],data2.value[39],
                            data2.value[40],data2.value[41],data2.value[42],data2.value[43],data2.value[44],data2.value[45],data2.value[46],data2.value[47],data2.value[48],data2.value[49],
                            data2.value[50],data2.value[51],data2.value[52],data2.value[53],data2.value[54],data2.value[55],data2.value[56],data2.value[57],data2.value[58],data2.value[59],
                            data2.value[60],data2.value[61],data2.value[62],data2.value[63],data2.value[64],data2.value[65],data2.value[66],data2.value[67],data2.value[68],data2.value[69],
                            data2.value[70],data2.value[71],data2.value[72],data2.value[73],data2.value[74],data2.value[75],data2.value[76],data2.value[77],data2.value[78],data2.value[79],
                            data2.value[80],data2.value[81],data2.value[82],data2.value[83],data2.value[84],data2.value[85],data2.value[86],data2.value[87],data2.value[88],data2.value[89],
                            data2.value[90],data2.value[91],data2.value[92],data2.value[93],data2.value[94],data2.value[95],data2.value[96],data2.value[97],data2.value[98],data2.value[99],
                            data2.value[100],data2.value[101],data2.value[102],data2.value[103],data2.value[104],data2.value[105],data2.value[106],data2.value[107],data2.value[108],data2.value[109],
                            data2.value[110],data2.value[111],data2.value[112],data2.value[113],data2.value[114],data2.value[115],data2.value[116],data2.value[117],data2.value[118],data2.value[119]]
                    }
                ]
            });
            num2.value++
        },30000)


        const res = await clientSysMen({
            ip: hostname.value
        })
        
        if(res){
            data2.value = res.data

            if(num2.value == 0){
                initEcharts2()
            }
        }
    }


    const getDiskPercent = async () => {
        clearTimeout(channel3.value)
        channel3.value = setTimeout(()=>{
            getDiskPercent()
            let echartsInfoOne3 = document.getElementById("echartsInfoOne3")
            let chart3 = echart.init(echartsInfoOne3);

            if(60 < data3.value.length) {
                data3.value.shift()
            }
            chart3.setOption({
                series: [
                    {
                        data: [data3.value[0],data3.value[1],data3.value[2],data3.value[3],data3.value[4],data3.value[5],data3.value[6],data3.value[7],data3.value[8],data3.value[9],
                            data3.value[10],data3.value[11],data3.value[12],data3.value[13],data3.value[14],data3.value[15],data3.value[16],data3.value[17],data3.value[18],data3.value[19],
                            data3.value[20],data3.value[21],data3.value[22],data3.value[23],data3.value[24],data3.value[25],data3.value[26],data3.value[27],data3.value[28],data3.value[29],
                            data3.value[30],data3.value[31],data3.value[32],data3.value[33],data3.value[34],data3.value[35],data3.value[36],data3.value[37],data3.value[38],data3.value[39],
                            data3.value[40],data3.value[41],data3.value[42],data3.value[43],data3.value[44],data3.value[45],data3.value[46],data3.value[47],data3.value[48],data3.value[49],
                            data3.value[50],data3.value[51],data3.value[52],data3.value[53],data3.value[54],data3.value[55],data3.value[56],data3.value[57],data3.value[58],data3.value[59],
                            data3.value[60],data3.value[61],data3.value[62],data3.value[63],data3.value[64],data3.value[65],data3.value[66],data3.value[67],data3.value[68],data3.value[69],
                            data3.value[70],data3.value[71],data3.value[72],data3.value[73],data3.value[74],data3.value[75],data3.value[76],data3.value[77],data3.value[78],data3.value[79],
                            data3.value[80],data3.value[81],data3.value[82],data3.value[83],data3.value[84],data3.value[85],data3.value[86],data3.value[87],data3.value[88],data3.value[89],
                            data3.value[90],data3.value[91],data3.value[92],data3.value[93],data3.value[94],data3.value[95],data3.value[96],data3.value[97],data3.value[98],data3.value[99],
                            data3.value[100],data3.value[101],data3.value[102],data3.value[103],data3.value[104],data3.value[105],data3.value[106],data3.value[107],data3.value[108],data3.value[109],
                            data3.value[110],data3.value[111],data3.value[112],data3.value[113],data3.value[114],data3.value[115],data3.value[116],data3.value[117],data3.value[118],data3.value[119]]
                    }
                ]
            });
            num3.value++
        },30000)


        const res = await clientSysDisk({
            ip: hostname.value
        })

        if(res){
            data3.value = res.data

            if(num3.value == 0){
                initEcharts3()
            }
        }
    }


    const initEcharts = () => {
        let echartsInfoOne = document.getElementById("echartsInfoOne")
        echartsInfoOne.removeAttribute("_echarts_instance_");
        let chart = echart.init(echartsInfoOne);
        chart.setOption({
            title: {
                text: 'cpu使用率',
                left: 'center'
            },
            xAxis: {
                type: 'category',
                boundaryGap: false,
                data: [1,2,3,4,5,6,7,8,9,10,12,12,13,14,15,16,17,18,19,20,31,32,33,34,35,36,37,38,39,40,41,42,43,44,45,46,47,48,49,50,51,52,53,54,55,56,57,58,59,60
                    ,61,62,63,64,65,66,67,68,69,70,71,72,73,74,75,76,77,78,79,80,81,82,83,84,85,86,87,88,89,90,91,92,93,94,95,96,97,98,99,100,101,102,103,104,105,106,107,108,109,110
                    ,111,112,113,114,115,116,117,118,119,120]
            },
            tooltip: {
                trigger: 'axis'
            },
            yAxis: {
                type: 'value'
            },
            grid: {
                left: '10%',
                right: '4%',
                bottom: '6%',
                containLabel: false
            },
            series: [
                {
                    symbol: "none",
                    name: '数量',
                    data: [data1.value[0],data1.value[1],data1.value[2],data1.value[3],data1.value[4],data1.value[5],data1.value[6],data1.value[7],data1.value[8],data1.value[9],
                        data1.value[10],data1.value[11],data1.value[12],data1.value[13],data1.value[14],data1.value[15],data1.value[16],data1.value[17],data1.value[18],data1.value[19],
                        data1.value[20],data1.value[21],data1.value[22],data1.value[23],data1.value[24],data1.value[25],data1.value[26],data1.value[27],data1.value[28],data1.value[29],
                        data1.value[30],data1.value[31],data1.value[32],data1.value[33],data1.value[34],data1.value[35],data1.value[36],data1.value[37],data1.value[38],data1.value[39],
                        data1.value[40],data1.value[41],data1.value[42],data1.value[43],data1.value[44],data1.value[45],data1.value[46],data1.value[47],data1.value[48],data1.value[49],
                        data1.value[50],data1.value[51],data1.value[52],data1.value[53],data1.value[54],data1.value[55],data1.value[56],data1.value[57],data1.value[58],data1.value[59],
                        data1.value[60],data1.value[61],data1.value[62],data1.value[63],data1.value[64],data1.value[65],data1.value[66],data1.value[67],data1.value[68],data1.value[69],
                        data1.value[70],data1.value[71],data1.value[72],data1.value[73],data1.value[74],data1.value[75],data1.value[76],data1.value[77],data1.value[78],data1.value[79],
                        data1.value[80],data1.value[81],data1.value[82],data1.value[83],data1.value[84],data1.value[85],data1.value[86],data1.value[87],data1.value[88],data1.value[89],
                        data1.value[90],data1.value[91],data1.value[92],data1.value[93],data1.value[94],data1.value[95],data1.value[96],data1.value[97],data1.value[98],data1.value[99],
                        data1.value[100],data1.value[101],data1.value[102],data1.value[103],data1.value[104],data1.value[105],data1.value[106],data1.value[107],data1.value[108],data1.value[109],
                        data1.value[110],data1.value[111],data1.value[112],data1.value[113],data1.value[114],data1.value[115],data1.value[116],data1.value[117],data1.value[118],data1.value[119]],
                    type: 'line',
                    
                }
            ]
        });
        window.onresize = function() {
            //自适应大小
            chart.resize();
        };
    }
    const initEcharts2 = () => {
        let echartsInfoOne = document.getElementById("echartsInfoOne2")
        echartsInfoOne.removeAttribute("_echarts_instance_");
        let chart = echart.init(echartsInfoOne);
        chart.setOption({
            title: {
                text: '内存使用率',
                left: 'center'
            },
            xAxis: {
                type: 'category',
                boundaryGap: false,
                data: [1,2,3,4,5,6,7,8,9,10,12,12,13,14,15,16,17,18,19,20,31,32,33,34,35,36,37,38,39,40,41,42,43,44,45,46,47,48,49,50,51,52,53,54,55,56,57,58,59,60
                    ,61,62,63,64,65,66,67,68,69,70,71,72,73,74,75,76,77,78,79,80,81,82,83,84,85,86,87,88,89,90,91,92,93,94,95,96,97,98,99,100,101,102,103,104,105,106,107,108,109,110
                    ,111,112,113,114,115,116,117,118,119,120]
            },
            tooltip: {
                trigger: 'axis'
            },
            yAxis: {
                type: 'value'
            },
            grid: {
                left: '10%',
                right: '4%',
                bottom: '6%',
                containLabel: false
            },
            series: [
                {
                    symbol: "none",
                    name: '内存使用率',
                    data: [data2.value[0],data2.value[1],data2.value[2],data2.value[3],data2.value[4],data2.value[5],data2.value[6],data2.value[7],data2.value[8],data2.value[9],
                            data2.value[10],data2.value[11],data2.value[12],data2.value[13],data2.value[14],data2.value[15],data2.value[16],data2.value[17],data2.value[18],data2.value[19],
                            data2.value[20],data2.value[21],data2.value[22],data2.value[23],data2.value[24],data2.value[25],data2.value[26],data2.value[27],data2.value[28],data2.value[29],
                            data2.value[30],data2.value[31],data2.value[32],data2.value[33],data2.value[34],data2.value[35],data2.value[36],data2.value[37],data2.value[38],data2.value[39],
                            data2.value[40],data2.value[41],data2.value[42],data2.value[43],data2.value[44],data2.value[45],data2.value[46],data2.value[47],data2.value[48],data2.value[49],
                            data2.value[50],data2.value[51],data2.value[52],data2.value[53],data2.value[54],data2.value[55],data2.value[56],data2.value[57],data2.value[58],data2.value[59],
                            data2.value[60],data2.value[61],data2.value[62],data2.value[63],data2.value[64],data2.value[65],data2.value[66],data2.value[67],data2.value[68],data2.value[69],
                            data2.value[70],data2.value[71],data2.value[72],data2.value[73],data2.value[74],data2.value[75],data2.value[76],data2.value[77],data2.value[78],data2.value[79],
                            data2.value[80],data2.value[81],data2.value[82],data2.value[83],data2.value[84],data2.value[85],data2.value[86],data2.value[87],data2.value[88],data2.value[89],
                            data2.value[90],data2.value[91],data2.value[92],data2.value[93],data2.value[94],data2.value[95],data2.value[96],data2.value[97],data2.value[98],data2.value[99],
                            data2.value[100],data2.value[101],data2.value[102],data2.value[103],data2.value[104],data2.value[105],data2.value[106],data2.value[107],data2.value[108],data2.value[109],
                            data2.value[110],data2.value[111],data2.value[112],data2.value[113],data2.value[114],data2.value[115],data2.value[116],data2.value[117],data2.value[118],data2.value[119]],
                    type: 'line',
                    
                }
            ]
        });
        window.onresize = function() {
            //自适应大小
            chart.resize();
        };
    }
    const initEcharts3 = () => {
        let echartsInfoOne = document.getElementById("echartsInfoOne3")
        echartsInfoOne.removeAttribute("_echarts_instance_");
        let chart = echart.init(echartsInfoOne);
        chart.setOption({
            title: {
                text: '磁盘使用率',
                left: 'center'
            },
            xAxis: {
                type: 'category',
                boundaryGap: false,
                data: [1,2,3,4,5,6,7,8,9,10,12,12,13,14,15,16,17,18,19,20,31,32,33,34,35,36,37,38,39,40,41,42,43,44,45,46,47,48,49,50,51,52,53,54,55,56,57,58,59,60
                    ,61,62,63,64,65,66,67,68,69,70,71,72,73,74,75,76,77,78,79,80,81,82,83,84,85,86,87,88,89,90,91,92,93,94,95,96,97,98,99,100,101,102,103,104,105,106,107,108,109,110
                    ,111,112,113,114,115,116,117,118,119,120]
            },
            tooltip: {
                trigger: 'axis'
            },
            yAxis: {
                type: 'value'
            },
            grid: {
                left: '10%',
                right: '4%',
                bottom: '6%',
                containLabel: false
            },
            series: [
                {
                    symbol: "none",
                    name: '磁盘使用率',
                    data: [data3.value[0],data3.value[1],data3.value[2],data3.value[3],data3.value[4],data3.value[5],data3.value[6],data3.value[7],data3.value[8],data3.value[9],
                            data3.value[10],data3.value[11],data3.value[12],data3.value[13],data3.value[14],data3.value[15],data3.value[16],data3.value[17],data3.value[18],data3.value[19],
                            data3.value[20],data3.value[21],data3.value[22],data3.value[23],data3.value[24],data3.value[25],data3.value[26],data3.value[27],data3.value[28],data3.value[29],
                            data3.value[30],data3.value[31],data3.value[32],data3.value[33],data3.value[34],data3.value[35],data3.value[36],data3.value[37],data3.value[38],data3.value[39],
                            data3.value[40],data3.value[41],data3.value[42],data3.value[43],data3.value[44],data3.value[45],data3.value[46],data3.value[47],data3.value[48],data3.value[49],
                            data3.value[50],data3.value[51],data3.value[52],data3.value[53],data3.value[54],data3.value[55],data3.value[56],data3.value[57],data3.value[58],data3.value[59],
                            data3.value[60],data3.value[61],data3.value[62],data3.value[63],data3.value[64],data3.value[65],data3.value[66],data3.value[67],data3.value[68],data3.value[69],
                            data3.value[70],data3.value[71],data3.value[72],data3.value[73],data3.value[74],data3.value[75],data3.value[76],data3.value[77],data3.value[78],data3.value[79],
                            data3.value[80],data3.value[81],data3.value[82],data3.value[83],data3.value[84],data3.value[85],data3.value[86],data3.value[87],data3.value[88],data3.value[89],
                            data3.value[90],data3.value[91],data3.value[92],data3.value[93],data3.value[94],data3.value[95],data3.value[96],data3.value[97],data3.value[98],data3.value[99],
                            data3.value[100],data3.value[101],data3.value[102],data3.value[103],data3.value[104],data3.value[105],data3.value[106],data3.value[107],data3.value[108],data3.value[109],
                            data3.value[110],data3.value[111],data3.value[112],data3.value[113],data3.value[114],data3.value[115],data3.value[116],data3.value[117],data3.value[118],data3.value[119]],
                    type: 'line',
                    
                }
            ]
        });
        window.onresize = function() {
            //自适应大小
            chart.resize();
        };
    }

    onUnmounted (()=>{
        clearTimeout(channel1.value)
        clearTimeout(channel2.value)
        clearTimeout(channel3.value)
    });

</script>


<style lang="scss" scoped>
.flex {
    margin-left: 40px;
}
.aaaa{
    width: 100%;
    display: flex;
    flex-wrap: wrap;
}

</style>
