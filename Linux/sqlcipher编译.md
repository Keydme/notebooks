```bash
sudo apt install libssl-dev libssl3 build-essential libcrypto openssl gcc-multilib
./configure --enable-tempstore=yes CFLAGS="-DSQLITE_HAS_CODEC" \
	LDFLAGS="-lcrypto"
make
```