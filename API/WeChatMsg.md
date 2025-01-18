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