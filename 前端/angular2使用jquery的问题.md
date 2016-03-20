# angular2开发时会遇到typings安装jquery，会编译出错#
## 问题描述：
**在我开发ａｎｇｕｌａｒ２和ａｎｇｕｌａｒ１混合开发时，ｔｙｐｉｎｇｓ安装angular.d.ts时要依赖jquery.td.ts**
**然而编译时会出错，因为angular2对$符号存在ｂｕｇ，导致编译不通过**

## 解决方案
#### 将jquery.d.ts中的
```
declare module "jquery" {
    export = $;
}
declare var jQuery: JQueryStatic;
declare var $: JQueryStatic;
```
#### 大概在３１９２行
#### 改为如下
```
interface JQuery {
    chosen(options?:any):JQuery;
}

declare module "jquery" {
    export = JQuery;
}
declare var jQuery: JQueryStatic;
```