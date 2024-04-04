
```js
(function (console) {
    console.save = function (data, filename) {
        let MIME_TYPE = "text/json";
        if (!data) return;
        if (!filename) filename = "console.json";
        if (typeof data === "object") data = JSON.stringify(data, null, 4);

        let blob = new Blob([data], { tyoe: MIME_TYPE });
        // 创建事件
        let e = document.createEvent("MouseEvent");
        // 创建一个a链接
        let a = document.createElement("a");
        // 设置a链接下载文件的名称
        a.download = filename;
        // 创建下载的URL对象（blob或者file）
        a.href = window.URL.createObjectURL(blob);
        a.dataset.downloadurl = [MIME_TYPE, a.download, a.href].join(":");
        // 初始化事件
        e.initMouseEvent("click", true, false, window, 0, 0, 0, 0, 0, false, false, false, false, 0, null);
        // 触发事件
        a.dispatchEvent(e);
    }
})(console)
var hi = JSON.parse(mbrowser.getHistories("", mbrowser.getCountHistories(), 0));
    console.save(hi,"History.txt");
```
只要在x浏览器历史记录页面输入这个就可以将历史记录导出
