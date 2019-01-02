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
      #加入新增按鈕及勾選框
      <td>
         <button v-on:click="addList(key)" type="button" class="btn btn-primary">增加</button>
            <input v-on:click="[item.checkbox?item.checkbox=false:item.checkbox=true]" type="checkbox"
            :checked="item.checkbox">
      </td>
</tr>
``` 
使用 methods 

全選
```
  allCheckBox(){
                // 判斷是否勾選全部
                if(this.allchackbox == true){
                    for(item  in this.listData){
                        this.listData[item].checkbox = true
                    }
                }else{
                    for(item  in this.listData){
                        this.listData[item].checkbox = false
                    }
                }
            },
```
新增500筆數
```
add500(){
        // 新增500筆
         var i = 0
         //從當前數據最後一筆開始新增
         for (item in this.listData){
             i++
         }

         var totel = i + 500 -1

         for (var v = i ; v <= total ; v++){
             this.listData.splice(v, 0, {
                  id: false,
                  title: '第'+ (v+1) +'筆',
                  checkbox: false,
                  edit: true,
                  })
             }
        },
```
新增選擇後一筆
```
   addList(key) {
                // 新增當下排序後一筆
                this.listData.splice(key + 1, 0, {
                    id: false,
                    title: '',
                    checkbox: false,
                    edit: true,
                })
            },
```
批次刪除
```
   delList() {
                this.loading = true;
                var delData = {}
                for (let i = this.listData.length - 1; i >= 0; i--) {
                    if (this.listData[i].checkbox) {
                        this.listData.splice(i, 1);
                        //delData[i] = this.listData[i]
                    }
                }
              }
```
點選批次編輯判斷
```
upList() {
           for (let i = this.listData.length - 1; i >= 0; i--) {
               if (this.listData[i].checkbox) {
                        this.listData[i].edit = true
               }
            }
         },
```
儲存編輯項目
```
setList() {
                this.loading = true;
                var setData = {}
                for (item in this.listData) {
                    if (this.listData[item].edit) {
                        if (this.listData[item].title == '') {
                            this.$message.error('欄位不可為空')
                            this.loading = false;
                            return false
                        } else {
                            this.listData[item].edit = false;
                            //setData[item] = this.listData[item]
                        }
                    }
                }
           }
```
