<template>
    <div class="line-container">
        <div id="line" class="line"></div>
    </div>
</template>

<script>
    import echarts from 'echarts/lib/echarts';
    // 引入柱状图
    import 'echarts/lib/chart/bar';
    import 'echarts/lib/chart/line';
    import 'echarts/lib/component/title';
    import 'echarts/lib/component/legend';
    import 'echarts/lib/component/toolbox';
    import 'echarts/lib/component/markPoint';
    import 'echarts/lib/component/tooltip';
    export default {
        name: "tendency",
        mounted() {
            this.fatChart = echarts.init(document.getElementById('line'));
            this.initData();
        },
        props: ['sevenDayData', 'sevenDay'],
        methods: {
            initData () {
                const colors = ['#5793f3', '#675bba', '#d14a61'];
                const option = {
                    color: colors,
                    title: {
                        text: '走势图',
                        subtext: ''
                    },
                    tooltip: {
                        trigger: 'axis'
                    },
                    legend: {
                        data:['新注册用户', '新增订单', '新增管理员']
                    },
                    toolbox: {
                        show: true,
                        feature: {
                            dataZoom: { yAxisIndex: 'none'},
                            dataView: {readOnly: false},
                            magicType: {type: ['bar', 'line']},
                            restore: {},
                        }
                    },
                    xAxis: {
                        type: 'category',
                        boundaryGap: false,
                        data: this.sevenDay
                    },
                    yAxis: [
                        {
                            type: 'value',
                            name: '用户',
                            min: 0,
                            max: 200,
                            position: 'left',
                            axisLine: {
                                lineStyle: {color: '#999'}
                            },
                            axisLabel: {formatter: '{value}'}
                        },
                        {
                            type: 'value',
                            name: '订单',
                            min: 0,
                            max: 200,
                            position: 'right',
                            axisLine: {
                                lineStyle: {color: '#999'}
                            },
                            axisLabel: {formatter: '{value}'}
                        }
                    ],
                    series: [
                        {
                            name: '新注册用户',
                            type: 'line',
                            data: this.sevenDayData[0],
                            yAxisIndex: 1,
                            markPoint: {
                                data: [
                                    {type: 'max', name: '最大值'},
                                    {type: 'min', name: '最小值'}
                                ]
                            }
                        },
                        {
                            name: '新增订单',
                            type: 'line',
                            data: this.sevenDayData[1],
                            yAxisIndex: 1,
                            markPoint: {
                                data: [
                                    {type: 'max', name: '最大值'},
                                    {type: 'min', name: '最小值'}
                                ]
                            }
                        },
                        {
                            name: '新增管理员',
                            type: 'line',
                            data: this.sevenDayData[2],
                            yAxisIndex: 1,
                            markPoint: {
                                data: [
                                    {type: 'max', name: '最大值'},
                                    {type: 'min', name: '最小值'}
                                ]
                            }
                        }
                    ]
                };
                this.fatChart.setOption(option);
            }
        },
        watch: {
            sevenDay: function () {
                this.initData()
            },
            sevenDayData: function () {
                this.initData()
            }
        }
    }
</script>

<style lang="scss" scoped>
@import "../styles/mixin";
    .line-container {
        display: flex;
        justify-content: center;
        .line {
            width: 90%;
            height: 450px;
        }
    }
</style>
