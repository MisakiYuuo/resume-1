<template id="style">
  <div id="content" class="styleEditor" ref="boxRefs">
    <pre>
      {{ code }}
    </pre>
  </div>

  <div class="resumeEditor">
    <pre>
      {{ rightContent }}
     </pre>

  </div>
  <div v-html="total"></div>

</template>

<script setup lang='ts'>
import { ref, computed, onMounted } from 'vue'
// 左边内容
let code = ref('')
let fCode = ref([
  `/*
* 参考: http://strml.net/
* 大家好，我是李旭东
* 这是我为进入新公司准备的简历。
* 说做就做！
*/

/* 首先给所有元素加上过渡效果 */
* {
  transition: all .3s;
}
/* 白色背景太单调了，我们来点背景 */
html {
  color: rgb(222,222,222); background: rgb(0,43,54);
}
/* 文字离边框太近了 */
.styleEditor {
  padding: .5em;
  border: 1px solid;
  margin: .5em;
  overflow: auto;
  width: 45vw; height: 90vh;
}
/* 代码高亮 */
.token.selector{ color: rgb(133,153,0); }
.token.property{ color: rgb(187,137,0); }
.token.punctuation{ color: yellow; }
.token.function{ color: rgb(42,161,152); }

/* 加点 3D 效果呗 */
html{
  perspective: 1000px;
}
.styleEditor {
  position: fixed; left: 0; top: 0;
  -webkit-transition: none;
  transition: none;
  -webkit-transform: rotateY(10deg) translateZ(-100px) ;
          transform: rotateY(10deg) translateZ(-100px) ;
}

/* 接下来我给自己准备一个编辑器 */
.resumeEditor{
  position: fixed; right: 0; top: 0;
  padding: .5em;  margin: .5em;
  width: 48vw; height: 90vh;
  border: 1px solid;
  background: white; color: #222;
  overflow: auto;
}
/* 好了，我开始写简历了 */


`,
  `
/* 这个简历好像差点什么
 * 对了，这是 Markdown 格式的，我需要变成对 HR 更友好的格式
 * 简单，用开源工具翻译成 HTML 就行了
 */
`
  ,
  `
/* 再对 HTML 加点样式 */
.resumeEditor{
  padding: 2em;
}
.resumeEditor h2{
  display: inline-block;
  border-bottom: 1px solid;
  margin: 1em 0 .5em;
}
.resumeEditor ul,.resumeEditor ol{
  list-style: none;
}
.resumeEditor ul> li::before{
  content: '•';
  margin-right: .5em;
}
.resumeEditor ol {
  counter-reset: section;
}
.resumeEditor ol li::before {
  counter-increment: section;
  content: counters(section, ".") " ";
  margin-right: .5em;
}
.resumeEditor blockquote {
  margin: 1em;
  padding: .5em;
  background: #ddd;
}
`])
//  ---------方法调用
// function makeResume() {
//  setTimeout(() => {
//    leftFn(0)
//  }, 20);
//  setTimeout(() => {
//   rtFn()
//  }, 20);
//  setTimeout(() => {
//    leftFn(1)
//  }, 20);

//   }

// makeResume()

new Promise(resolve => {
  setTimeout(() => {
    leftFn(0)
    resolve(1);
  }, 100);
}).then(val => {
  setTimeout(() => {
    rtFn()
  }, 55000);
});




// -----右边内容
let rightContent = ref('')
let rightCh = ref(`姓名:李旭东
----

前端工程师。

技能
----

* 前端开发


对租赁软件的理解
----
第一种:类似于传统租赁行业的
1. 便利性:租赁 app 为用户提供了快捷、方便的租赁体验,用户可以在手机上轻松搜索、预订和管理租赁物品,大大提高了租赁效率。

2. 信息透明:租赁 app 通常会提供物品的详细信息、价格、评价等,帮助用户做出更明智的租赁决策。同时也为租赁商家提供了展示和营销的平台。

3. 灵活性:租赁 app 允许用户根据需求临时租赁物品,无需长期承担购买成本,符合当下共享经济的趋势。

4. 安全性:优秀的租赁 app 会有完善的信用评价系统和纠纷处理机制,提高了交易的安全性。

5. 数据应用:租赁 app 积累的用户行为数据,可以帮助优化产品和服务,提升用户体验。

总的来说,租赁 app 为用户提供了更加便捷、灵活的租赁服务,在满足个人需求的同时,也带动了共享经济的发展。未来随着技术的进步,租赁 app 必将有更多创新应用。
----
第二种:saas系统
1. 基于云计算的软件交付模式:SaaS 系统是通过互联网以订阅的方式提供软件服务,用户无需安装和维护本地软件,而是通过浏览器或移动应用访问云端的软件。

2. 按需使用和按需付费:SaaS 系统采用按需使用和按需付费的模式,用户可根据实际需求灵活选择功能和服务,并按实际使用情况支付费用,无需一次性大额投入。

3. 集中管理和自动更新:SaaS 供应商负责软件的集中管理和自动更新,用户可以随时获得最新版本的软件,无需自行升级。这大大降低了用户的 IT 管理成本。

4. 可扩展性和灵活性:SaaS 系统基于云架构,具有良好的可扩展性,可根据用户需求灵活调整资源配置。同时也支持跨设备、跨地域的访问。

5. 数据安全性:SaaS 供应商通常具有专业的数据安全管理能力,能够为用户提供更加可靠的数据安全保障。

总的来说, SaaS 系统具有使用便利性、成本节约、灵活性和安全性等优势,越来越受到企业和个人用户的青睐。随着云计算技术的不断发展,SaaS 必将在未来扮演更加重要的角色。


`)
// --------
let boxRefs = ref(null)
// onMounted(()=>{

// goBottom()
// })
// function goBottom(){
//   // console.log(boxRefs.value);
//   if(boxRefs.value){boxRefs.value.scrollTop = 100000}else{
//     boxRefs.value = null
//   }


// }
// ----------

let total = computed(() => {
  return '<style>' + code.value + '</style>'
})
function leftFn(nu: number) {

  let n = ref(0)
  setInterval(() => {
    code.value = fCode.value[nu].substring(0, n.value)
    n.value++

  }, 50)
}

function rtFn() {
  let n = ref(0)
  setInterval(() => {
    rightContent.value = rightCh.value.substring(0, n.value)
    n.value++
  }, 50)

}


</script>

<style>
pre {
  white-space: pre-wrap;
  white-space: -moz-pre-wrap;
  white-space: -pre-wrap;
  white-space: -o-pre-wrap;
  word-wrap: break-word;
}


/* code{
  background-color: red
 } */
/*  */
</style>