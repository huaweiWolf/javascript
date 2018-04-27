# 函数节流

在浏览器 DOM 事件里面，有一些事件会随着用户的操作不间断触发。比如：重新调整浏览器窗口大小（resize），浏览器页面滚动（scroll），鼠标移动（mousemove）。也就是说用户在触发这些浏览器操作的时候，如果脚本里面绑定了对应的事件处理方法，这个方法就不停的触发。

这并不是我们想要的，因为有的时候如果事件处理方法比较庞大，DOM 操作比如复杂，还不断的触发此类事件就会造成性能上的损失，导致用户体验下降（UI 反映慢、浏览器卡死等）

### 函数节流的实现：
延时delay执行，每隔interval必须执行一次（控制执行频率）
<pre>
var count = 0;

function fn() {
    document.getElementById("resultId").innerHTML += "第" + ++count + "次执行</br>";
}

function throttle(fn, delay, interval) {
    var timeId = null,
        lastTime = null;
    return function() {
        var timeNow = new Date().getTime();
        if (!lastTime) lastTime = timeNow;
        clearTimeout(timeId);
        if (interval && (timeNow - lastTime) > interval) {
            fn();
            lastTime = timeNow;
        } else {
            timeId = setTimeout(fn, delay);
        }
    };
}
//window.onscroll = throttle(fn, 200);
window.onscroll = throttle(fn, 200, 1000);
</pre>
