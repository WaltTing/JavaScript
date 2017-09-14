# 常见JS类型转换表
值|to 字符串|to 数字|to 布尔值|to 对象
-|-|-|-|-
undefined|"undefined"|NaN|false|Type Error
null|"null"|0|false|Type Error
true|"true"|1||new Boolean(true)
false|"false"|0||new Boolean(true)
""||0|false|new String("")
"1.2"||1.2|true|new String("1.2")
"one"||NaN|true|new String("one")
0|"0"||false|new Number(0)
-0|"0"||false|new Number(-0)
NaN|"NaN"||false|new Number(NaN)
Infinity|"Infinity"||true|new Number(Infinity)
-Infinity|"-Infinity"||true|new Number(-Infinity)
{}|||true|
[]|""|0|true|
[9]|"9"|9|true|
['a']|使用join方法|NaN|true
function(){}||NaN|true

## 补充：
  console.log("a"+1); //a1                     
  console.log("a"-a); //NaN                        
  console.log('a'-1); //NaN                         
  console.log('a'+1); //a1 
  
更多内容待更新。。。。。。
