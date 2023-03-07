# 模板字符串替换

## 二月

```javascript
  let str = "{{name}}很厉害，才{{age}}岁"
  let obj = {name: '二月', age: 15}
  function test(str, obj){
    let _s = str.replace(/\{\{(\w+)\}\}/g, '$1')
    let result
    for(let k in obj) {
      // 应该替换 `{{${k}}}`
      _s = _s.replace(new RegExp(k, 'g'), obj[k])
    }
  return _s
  }
  const s = test(str, obj)

```

**/\{\{(\w+)\}\}/** : 匹配双括号里面的值

## 志钦

```javascript
  var str = "{{name}}很厉害，才{{age}}岁";
  var str2 = "{{name}}很厉name害，才{{age}}岁{{name}}";

  var obj = {name: '周杰伦', age: 15};
  function fun(str, obj) {
      var arr;
      arr = str.match(/{{[a-zA-Z\d]+}}/g);
      for(var i=0;i<arr.length;i++){
          arr[i] = arr[i].replace(/{{|}}/g,'');
          str = str.replace('{{'+arr[i]+'}}',obj[arr[i]]);
      }
      return str;
  }
  console.log(fun(str,obj));
  console.log(fun(str2,obj));
```

**/{{[a-zA-Z\d]+}}/** : a-z A-Z 数字 一次或者多次

## 小维

```javascript
  function a(str, obj) {
    var str1 = str;
    for (var key in obj) {
      var re = new RegExp("{{" + key + "}}", "g");
      str1 = str1.replace(re, obj[key]);
    }
    console.log(str1);
  }
  const str = "{{name}}很厉name害{{name}}，才{{age}}岁";
  const obj = { name: "jawil", age: "15" };
  a(str, obj);

```

**/`{{${key}}}`/** : 匹配具体的key值

## 最终

```javascript
  function render(template, context) {
    return template.replace(/\{\{(.*?)\}\}/g, (match, key) => context[key.trim()]);
  }
  const template = "{{name   }}很厉name害，才{{age   }}岁";
  const context = { name: "jawil", age: "15" };
  console.log(render(template, context));
```

```javascript

  String.prototype.render = function (context) {
    return this.replace(/{{(.*?)}}/g, (match, key) => context[key.trim()]);
  };
  
```

**/\{\{(.*?)\}\}/** : (.*?)代表非贪婪匹配分组，查询任意字符， 匹配一次结束