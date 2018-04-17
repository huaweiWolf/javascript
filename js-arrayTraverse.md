# js多维数组遍历

## 方法1：全局变量
<pre>
var arr = [1, 2, ["3", 4, "5", [6, ["7", 8]]]];
function flat(arr) {
    var j = 0;
    var arrRes = [];

    function arrChange(arr) {
        for (var i = 0; i < arr.length; i++) {
            if (arr[i].constructor == Array) {
                arrChange(arr[i]);
            } else {
                arrRes[j++] = arr[i];
            }
        }
    }
    arrChange(arr);
    return arrRes;
}
console.log(flatMethod(arr));
</pre>

## 方法2：复写each方法
<pre>
var arr = [1, 2, ["3", 4, "5", [6, ["7", 8]]]];
Array.prototype.each = function (fn) {
    this.i = 0;
    if (this.length > 0 && fn.constructor == Function){
        while (this.i < this.length) {
            var ele = this[this.i];
            if (ele.constructor == Array) {
                ele.each(fn);
            } else {
                fn.call(ele, ele);
            }
            this.i++;
        }
        this.i = null;
    }
}

function flatMethod(arr) {
    var arrRes = [], i = 0;
    arr.each(function(item){
        arrRes[i++] = item;
    });
    return arrRes;
}
console.log(flatMethod(arr));
</pre>
