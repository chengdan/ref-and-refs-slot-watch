#ref $refs

如果在元素中加上ref属性

    1. 该元素是一个普通的dom元素
        会将当前的dom元素的dom对象以ref属性的值作为属性名加入到当前元素所在vue实例的$refs对象中去
    2. 该元素是一个组件元素
        会将当前的元素的组件对象以ref属性的值作为属性名加入到当前元素所在vue实例的$refs对象中去

不常用！

#插槽

是一个slot标签，可以插入到需要插入的位置，如果DOM标签里写了slot属性，slot标签里设置的name属性的值要与DOM里slot属性的值一致，这样就可以将内容插入到对应的位置中

具名插槽

    <mycomp><button slot="名字"></button></mycomp>

    Vue.component("mycomp", {
        template: "<div> <slot name='名字'></slot> </div>"
    })
    
```html
<div id="app">
    <!--这里不写slot="first"这个控制台会报错，但是内容还是会展示出来-->
    <!--<mycomp><button>第一个按钮</button><button>第二个按钮</button></mycomp>-->
    <mycomp><button slot="second">第一个按钮</button><button slot="first">第二个按钮</button></mycomp>
</div>
```
```javascript
//这里不写<slot></slot>标签上面的button里面的内容就无法显示
    Vue.component('mycomp',{
        template :"<div><slot name='first'></slot>我是组件里面的内容<slot name='second'></slot></div>"
    })
    let vm = new Vue({
        el:'#app',
        data:{

        }
    })
```
#watch

watch可以用来监听数据的变化

```html
<div id="app">
    <!--<input type="text" v-model="msg">-->
    <input type="text" v-model="person.money">
</div>
```

```javascript
let vm = new Vue({
        el:'#app',
        data:{
            msg : '老王是最危险的男人',
            person:{
                name : '老王',
                money : 100
            }
        },
        watch :{
            msg : function (newValue,oldValue) {
                console.log('老王被动了！！！');
            },
            person:{
                handler:function (newValue,oldValue) {
//                    console.log(newValue, oldValue);
                    console.log('老王的钱被动了哈哈哈哈')
                },
                //写了deep后才能深度监视，否则改变老王的钱数是没办法检测的
                deep:true,
                //immediate表示当监视生效的时候，直接执行一次函数
                immediate:true
            }
        }
    })
```


