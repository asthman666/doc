# Click    
    
    <html>
        <body>
            <button id="go">Go</button>
            <script>
                function go() {
                    console.log("go");
                }
                document.querySelector("#go").addEventListener("click",go)
                document.querySelector("#go").addEventListener("click", go)                         
                //document.querySelector("#go").removeEventListener("click",go)         
            </script>
        </body>
    </html>

绑定两次click时，点击`Go`，会调用两次go方法

尽量避免重复绑定

> [addEventListener的第三个参数](https://blog.csdn.net/sunrunning/article/details/80199842)

> [events_order](https://www.quirksmode.org/js/events_order.html#link4)

> [addEventListener](https://developer.mozilla.org/zh-CN/docs/Web/API/EventTarget/addEventListener)

> [removeEventListener](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/removeEventListener)