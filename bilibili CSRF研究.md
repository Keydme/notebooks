算了
```js
function V(t) {
	return new Promise((function(e) {
		if (p)
			e("");
		else {
			var n = b("bili_jct", t);
			d ? l(A).then((function(t) {
				t ? f.callNative({
					method: A,
					callback: function(t) {
						e(t.csrf)
					}
				}) : e(n)
			}
			)) : e(n)
		}
	}
	))
}
```

```js
b = function(t, e) {
                    var n = "";
                    if (p && !e)
                        return n;
                    var r = e || document.cookie;
                    if (!r)
                        return n;
                    for (var i = r.split(";"), o = new RegExp("^".concat(t, "=")), a = 0; a < i.length; a++) {
                        var s = i[a].trim();
                        if (o.test(s)) {
                            n = s.split("=")[1];
                            break
                        }
                    }
                    return n
                }
```

```json
#recieve data json
{
"code":0,
"message":"0",
"ttl":1,
"data":
	{
	"activity_id":2804,
	"activity_name":"星穹铁道2.0激励计划",
	"receive_time":1707400661,
	"type":"CdKeyV2",
	"name":"CdKeyV2",
	"icon":"https://i0.hdslb.com/bfs/activity-plat/static/b9vgSxGaAg.png",
	"extra":
		{
		"MultiLife":"true",
		"cdkey_content":"HTSW72ZXZSA8",
		"cdkey_id":"8561996"
		},
	"award_id":19859,
	"mid":3546557704046966,
	"description":"",
	"pre_check_ok":true,
	"pre_check_msg":"",
	"send_extra":
		{
		"MultiLife":"true",
		"cdkey_content":"HTSW72ZXZSA8",
		"cdkey_id":"8561996"
		},
	"pre_check_error_type":"",
	"unique_id":"mis-03-066-700386"
	}
}
```