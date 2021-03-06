:::demo - 通过设置 `loading-content` 自定义loading效果<br> - 通过设置 `error-content` 自定义失败效果
```html
<template>
    <div>
        <input type="button" value="重新请求" @click="request()"/>

        <v-table
                is-horizontal-resize
                :loading-content="loadingContent"
                :error-content="errorContent"
                :is-loading="isLoading"
                style="width:100%"
                :columns="columns"
                :table-data="tableData"
        ></v-table>
    </div>
</template>

<script>

    export default{
        data() {
            return {
                loadingContent:'<span>加载中...</span>',
                errorContent:'<a href="javascript:void(0);">刷新重试</a>',
                isLoading: true, // 是否正在加载中
                tableData: [],
                columns: [
                    {field: 'name', title: '姓名', width: 80, titleAlign: 'center', columnAlign: 'center',isResize: true},
                    {field: 'tel', title: '手机号码', width: 80, titleAlign: 'center', columnAlign: 'center',isResize: true},
                    {field: 'hobby', title: '爱好', width: 80, titleAlign: 'center', columnAlign: 'center',isResize: true},
                    {field: 'address',title: '地址', width: 280,titleAlign: 'center',columnAlign: 'left',isResize: true}
                ]
            }
        },
        methods: {

            request(){
                this.isLoading = true;

                var r = Math.random();

                setTimeout(x => {
                    this.isLoading = false;

                    if (r > 0.5) {
                        this.tableData = [];
                    } else {
                        this.tableData = [
                            {"name":"赵伟","tel":"156*****1987","hobby":"钢琴、书法、唱歌","address":"上海市黄浦区金陵东路569号17楼"},
                             {"name":"李伟","tel":"182*****1538","hobby":"钢琴、书法、唱歌","address":"上海市奉贤区南桥镇立新路12号2楼"},
                             {"name":"孙伟","tel":"161*****0097","hobby":"钢琴、书法、唱歌","address":"上海市崇明县城桥镇八一路739号"},
                             {"name":"周伟","tel":"197*****1123","hobby":"钢琴、书法、唱歌","address":"上海市青浦区青浦镇章浜路24号"},
                             {"name":"吴伟","tel":"183*****6678","hobby":"钢琴、书法、唱歌","address":"上海市松江区乐都西路867-871号"}
                        ];
                    }

                }, 3000);
            }
        },

        created(){

            this.request();
        }
    }
</script>
```
:::