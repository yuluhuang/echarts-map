<template>
    <div class="home">
        <div ref="two" style="height: 700px; width: 100%;"></div>
    </div>
</template>

<script>
    // @ is an alias to /src
    import echarts from 'echarts'
    import {MP} from '../MP.js'
    require('echarts/extension/bmap/bmap')
    export default {
        name: 'home',
        data () {
            return {
                result: require('../assets/rightTop.json'),
                chart2: null,
                bmao_contry_data: [],
                bmap_hzs_data: []
            }
        },
        mounted: function () {
            const self = this
            self.$nextTick(function () {
                if (window.BMap) {
                    self.BMap = window.BMap
                    self.init_chart(window.BMap)
                    return
                }
                MP('G0cTfLmvMdmb6x2QLSGnoTM7piZOfGGu').then(function (BMap) {
                    // 在此调用api
                    window.BMap = BMap
                    self.init_chart(BMap)
                })
            })
        },
        methods: {
            init_chart (BMap) {
                const self = this
                let myFirstPromise = new Promise(function (resolve) {
                    self.result.result.forEach(function (v) {
                        self.bmao_contry_data.push({name: v.name, value: v.sum, type: 'country'})
                        v.type.forEach(function (v1) {
                            self.bmap_hzs_data.push({name: v1.name, value: [v1.coordinate[0], v1.coordinate[1], (v1.value > 1000 ? 1000 : v1.value) * 500], type: 'hzs'})
                        })
                    })
                    resolve()
                })

                myFirstPromise.then(function () {
                    self.init_xixiu_chart(BMap)
                })
            },
            init_xixiu_chart () {
                const self = this
                self.chart2 = echarts.init(this.$refs.two)
                var option = {
                    backgroundColor: 'white',
                    title: {
                        text: '',
                        x: 'center'
                    },
                    tooltip: {
                        trigger: 'item',
                        formatter: '{b}'
                    },
                    bmap: {
                        center: [106.067975, 26.201887], // + 左,  - 上
                        zoom: 11,
                        enableMapClick: false,
                        roam: false,
                        mapStyle: {
                            styleJson: [
                                {
                                    'featureType': 'water',
                                    'elementType': 'all',
                                    'stylers': {
                                        backgroundColor: 'white',
                                        color: 'white',
                                        'visibility': 'off'

                                    }
                                },
                                {
                                    'featureType': 'land',
                                    'elementType': 'all',
                                    'stylers': {
                                        backgroundColor: 'white',
                                        color: 'white',
                                        'visibility': 'off'
                                    }
                                },
                                {
                                    'featureType': 'boundary',
                                    'elementType': 'geometry',
                                    'stylers': {
                                        backgroundColor: 'white',
                                        color: 'white',
                                        'visibility': 'off'
                                    }
                                },
                                {
                                    'featureType': 'railway',
                                    'elementType': 'all',
                                    'stylers': {
                                        backgroundColor: 'white',
                                        color: 'white',
                                        'visibility': 'off'
                                    }
                                },
                                {
                                    'featureType': 'highway',
                                    'elementType': 'geometry',
                                    'stylers': {
                                        backgroundColor: 'white',
                                        color: 'white',
                                        'visibility': 'off'
                                    }
                                },
                                {
                                    'featureType': 'highway',
                                    'elementType': 'geometry.fill',
                                    'stylers': {
                                        backgroundColor: 'white',
                                        color: 'white',
                                        'visibility': 'off'
                                    }
                                },
                                {
                                    'featureType': 'highway',
                                    'elementType': 'labels',
                                    'stylers': {
                                        backgroundColor: 'white',
                                        color: 'white',
                                        'visibility': 'off'
                                    }
                                },
                                {
                                    'featureType': 'arterial',
                                    'elementType': 'geometry',
                                    'stylers': {
                                        backgroundColor: 'white',
                                        color: 'white',
                                        'visibility': 'off'
                                    }
                                },
                                {
                                    'featureType': 'arterial',
                                    'elementType': 'geometry.fill',
                                    'stylers': {
                                        backgroundColor: 'white',
                                        color: 'white',
                                        'visibility': 'off'
                                    }
                                },
                                {
                                    'featureType': 'poi',
                                    'elementType': 'all',
                                    'stylers': {
                                        backgroundColor: 'white',
                                        color: 'white',
                                        'visibility': 'off'
                                    }
                                },
                                {
                                    'featureType': 'green',
                                    'elementType': 'all',
                                    'stylers': {
                                        backgroundColor: 'white',
                                        color: 'white',
                                        'visibility': 'off'
                                    }
                                },
                                {
                                    'featureType': 'subway',
                                    'elementType': 'all',
                                    'stylers': {
                                        backgroundColor: 'white',
                                        color: 'white',
                                        'visibility': 'off'
                                    }
                                },
                                {
                                    'featureType': 'manmade',
                                    'elementType': 'all',
                                    'stylers': {
                                        backgroundColor: 'white',
                                        color: 'white',
                                        'visibility': 'off'
                                    }
                                },
                                {
                                    'featureType': 'local',
                                    'elementType': 'all',
                                    'stylers': {
                                        backgroundColor: 'white',
                                        color: 'white',
                                        'visibility': 'off'
                                    }
                                },
                                {
                                    'featureType': 'arterial',
                                    'elementType': 'labels',
                                    'stylers': {
                                        backgroundColor: 'white',
                                        color: 'white',
                                        'visibility': 'off'
                                    }
                                },
                                {
                                    'featureType': 'boundary',
                                    'elementType': 'geometry.fill',
                                    'stylers': {
                                        backgroundColor: 'white',
                                        color: 'white',
                                        'visibility': 'off'
                                    }
                                },
                                {
                                    'featureType': 'building',
                                    'elementType': 'all',
                                    'stylers': {
                                        backgroundColor: 'white',
                                        color: 'white',
                                        'visibility': 'off'
                                    }
                                },
                                {
                                    'featureType': 'label',
                                    'elementType': 'all',
                                    'stylers': {
                                        'visibility': 'off'
                                    }
                                }
                            ]
                        }
                    },
                    dataRange: {
                        show: false,
                        min: 0,
                        max: 8000,
                        x: 'left',
                        y: 'bottom',
                        text: ['高', '低'],           // 文本，默认为数值文本
                        calculable: true,
                        inRange: {
                            color: ['#819FF7', '#0404B4', 'yellow']
                        }
                    },
                    toolbox: {
                        show: false,
                        orient: 'vertical',
                        x: 'right',
                        y: 'center',
                        feature: {
                            mark: {
                                show: true
                            },
                            dataView: {
                                show: true,
                                readOnly: false
                            },
                            restore: {
                                show: true
                            },
                            saveAsImage: {
                                show: true
                            }
                        }
                    },
                    series: [
                        {
                            name: '合作社',
                            type: 'scatter',
                            coordinateSystem: 'bmap',
                            data: self.bmap_hzs_data,
                            symbolSize: function (val) {
                                return val[2] / 10000
                            },
                            label: {
                                normal: {
                                    formatter: '{b}',
                                    //                                position: 'center',
                                    show: false,
                                    position: 'inside',
                                    color: 'red'
                                },
                                emphasis: {
                                    show: false
                                }
                            },
                            itemStyle: {
                                normal: {
                                    color: 'green'
                                }
                            }
                        },
                        {
                            name: '乡镇',
                            type: 'map',
                            map: 'xixiu',
                            mapType: '安顺市',
                            selectedMode: 'single',
                            roam: false,
                            itemStyle: {
                                normal: {label: {show: true}},
                                emphasis: {label: {show: true}}
                            },
                            tooltip: {
                                trigger: 'item',
                                formatter: '种植面积: {c} 亩'
                            },
                            label: {
                                normal: {
                                    formatter: '{b}',
                                    //                                position: 'center',
                                    show: true,
                                    position: 'inside'
                                },
                                emphasis: {
                                    show: true
                                }
                            },
                            lableLine: {
                                normal: {
                                    show: true
                                },
                                emphasis: {
                                    show: true
                                }
                            },
                            data: self.bmao_contry_data
                        }
                    ]
                }
                echarts.registerMap('xixiu', require('../assets/520402.json'))
                self.chart2.setOption(option)
            },
        },
        components: {}
    }
</script>
