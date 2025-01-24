frida -U -f com.tencent.mm -l fp.js --no-pause


编译解码
PRAGMA key = '97e1680';
PRAGMA cipher_use_hmac = off;
PRAGMA kdf_iter = 4000;
PRAGMA cipher_page_size = 1024;
PRAGMA cipher_hmac_algorithm = HMAC_SHA1;
PRAGMA cipher_kdf_algorithm = PBKDF2_HMAC_SHA1;
ATTACH DATABASE 'plaintext.db' AS plaintext KEY '';
SELECT sqlcipher_export('plaintext');
DETACH DATABASE plaintext;

查表
select * from message limit 1;

```python
def decode(fn,psd=""):
    conn = sqlite.connect(fn)
    c = conn.cursor()
    command_list = [f"PRAGMA key='{psd}';",
                    'PRAGMA cipher_use_hmac = off;',
                    'PRAGMA kdf_iter = 4000;',
                    'PRAGMA cipher_page_size = 1024;',
                    'PRAGMA cipher_hmac_algorithm = HMAC_SHA1;',
                    'PRAGMA cipher_kdf_algorithm = PBKDF2_HMAC_SHA1;',
                    "ATTACH DATABASE 'plaintext2.db' AS plaintext KEY '';",
                    "SELECT sqlcipher_export('plaintext');",
                    "DETACH DATABASE plaintext;"]
    for cmd in command_list:
        c.execute(cmd)
```

```python
# 几大文件的存储位置
#### 关于鄙人微信手机备份copy
prefix = ['/data/data/com.tencent.mm/MicroMsg/{}/','/sdcard/Android/data/com.tencent.mm/MicroMsg/{}/']
suffix = ['image2','avator','EnMicroMsg.db','WxFileIndex.db','voice2','voide','Download']
wx_file_path = [prefix[i//4]+suffix[i] for i in range(7)]
# 1,1
# 5,2
class WeBackUp():
    def __init__(self,uid='',psd=''):
        if not uid:
            pass
        if not psd:
            pass

```
未完待续。。。