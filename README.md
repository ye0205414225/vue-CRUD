# vue-CRUD
Vue 前端基本 CRUD 操作課程

![image](https://github.com/ye0205414225/vue-CRUD/blob/master/%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202019-01-02%20%E4%B8%8A%E5%8D%889.51.22.png)
``` 
# 先設定按鈕function
<button v-on:click="setList()" type="button" class="btn btn-secondary">儲存</button>
<button v-on:click="upList()" type="button" class="btn btn-info">編輯</button>
<button v-on:click="delList()" type="button" class="btn btn-danger">刪除</button>
<button v-on:click="add500()" type="button" class="btn btn-secondary">新增500筆</button>
# 設定 checkbox
<th scope="col">操作
   <input v-model="allchackbox" v-on:change="allCheckBox()" type="checkbox" :checked="allchackbox">
</th>
# 設定 新增function
<button v-on:click="addList(key)" type="button" class="btn btn-primary">增加</button>
```
宣告 使用vuejs
宣告 預處理 變數資料
``` 
 var app = new Vue({
        el: '#vueContent',
        data: {
            loading: true,      // 載入
            listData: [],       // 列表
            allchackbox:false,  // 批次勾選
        },
     });
```
使用 mounted function 預先寫入數據
``` 
mounted() {

            // 預先載入處理資料 json 物件
            this.listData = [
                {
                    id: false,
                    title: '',
                    checkbox: false,
                    edit: true,
                },
                {
                    id: false,
                    title: '啊啊啊啊',
                    checkbox: false,
                    edit: false,
                },
                {
                    id: false,
                    title: '喔喔喔喔',
                    checkbox: false,
                    edit: false,
                },
            ]
        }
```
使用v-for迴圈 列出 listData 內的資料
``` 
<tr v-for="(item,key,arr) in listData">
   <th scope="row">{{ key+1 }}</th>
      <td>
         <template v-if="item.edit">
            <input v-model="item.title" type="text" class="form-control">
         </template>
         <template v-else>
             {{ item.title }}
         </template>
      </td>
      <td>
         <button v-on:click="addList(key)" type="button" class="btn btn-primary">增加</button>
            <input v-on:click="[item.checkbox?item.checkbox=false:item.checkbox=true]" type="checkbox"
            :checked="item.checkbox">
      </td>
</tr>
``` 
