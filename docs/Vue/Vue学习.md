[TOC]

# 1. vm.$emit( event, arg ) //触发当前实例上的事件

### 2. vm.$on( event, fn );//监听event事件后运行 fn； 

### 3. 关于遮罩问题

```vue
<el-dialog ref="dialog" :title="title" :visible.sync="addDialog" @close="$reset('form')" :width="width"
:close-on-click-modal='false' append-to-body="true" ></el-dialog>
```

![image-20200825083401511](F:\WorkDocument\我的坚果云\note\images\image-20200825083401511.png)

### 4. Vue项目 报错TypeError [ERR INVALID ARG TYPE]: The “path“ argument must be of type string

![image-20200904085844881](F:\WorkDocument\我的坚果云\note\images\image-20200904085844881.png)

原因：sassloader版本过高导致的

解决方法: 回退7.×版本
**npm uninstall sass-loader（卸载当前版本）**

**npm install sass-loader@7.3.1 --save-dev**

### 5. this.$nextTick()等待dom生成以后再来获取dom对象,在进行其他具体操作

### 6. 关于加载问题

```js
async getUser () {
    await this.$api.userMgr.getUserList().then(res => {
        const {data} = res
        if (data.success) {
            this.userList = data.results
        } else {
            this.$message.error(data.msg)
        }
    })
},
```

```js
 _this.getUser().then(res => {
  _this.initHandle()
 })
```

### 7. 如果select绑定的值为对象，请务必指定value-key为它的唯一性标示

```vue
data(){
　　return{
　　　　test:'',
　　　　arr:[{id:1,name:'张三'},{id:2,name:'李四'},{id:3,name:'王五'}]
　　}
}
<el-select v-model="test" value-key="id">
　　<el-option v-for="item in arr" :label="item.name" :key="item.id" :value="item"></el-option>
</el-select>
```

### 8.动态指令参数

Vue 2.6的最酷功能之一是可以将指令参数动态传递给组件。假设你有一个按钮组件，并且在某些情况下想监听单击事件，而在其他情况下想监听双击事件。这就是这些指令派上用场的地方：

```vue
<template>
    ...
    <aButton @[someEvent]="handleSomeEvent()" />...
</template>
<script>
  ...
  data(){
    return{
      ...
      someEvent: someCondition ? "click" : "dbclick"
    }
  },
  methods: {
    handleSomeEvent(){
      // handle some event
    }
  }  
</script>
```

而且，这实际上也很整洁-你可以将相同的模式应用于动态HTML属性，props等

### 9.通过axios下载

在使用axios请求的时候，加上`responseType: 'blob'`入参

```js
  download (ids) {
    return axios({
      url: FILE_SERVICE_MOCK_ROUTE + '/file/download/' + ids,
      method: 'get',
      responseType: 'blob'
    })
  }
```

```js
downFile (fileId, name) {
    this.$api.fileService.downloadById(fileId).then(res => {
    window.downFile(res.data, '文件下载')
    // this.fileUrl = window.URL.createObjectURL(new File([res.data], name))
    // const link = document.createElement('a')
    // link.href = this.fileUrl
    // link.setAttribute('download', name)
    // document.body.appendChild(link)
    // link.click()
    // link.remove()
    })
}
```

### 10. 关闭el-drawer默认选中title

```css
/*去掉打开抽屉时自动选中标题时的蓝色边框*/
.el-drawer__header span:focus {
    outline: 0;
}
```

### 11. `el-tree`树加载完成后点击

```js
 this.$nextTick(() => {
 	document.querySelector('.el-tree-node__content').click();
 });
```

### 12. 关于Node发布

```bash
1. 在 package.json 中，修改新发布的版本号
2. 打包
    npm run lib
3. 登录Nexus
    npm login
4. 发布
    npm publish
5. 卸载依赖
	npm uninstall avue-form-design
6. 重新安装
	npm install avue-form-design --save
```

### 13. Vue3 中关于路由参数获取

```typescript
<script lang="ts" setup>
import { onMounted } from "vue";
import { useRouter } from "vue-router";
const router = useRouter()
onMounted(()=>{
  let   data  = router.currentRoute.value.params.id
  console.log('data',data);
})
</script>
```

