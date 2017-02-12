# telegram-cli-mac
Precompiled Telegram binaries for MacOS.

It's really tricky to get this stupid thing compiled on MacOS. If trust is a heavy issue for you, maybe go the long route, but here's how I compiled them:

```bash
git clone --recursive https://github.com/vysheng/tg.git && cd tg
brew install libconfig readline lua python libevent jansson openssl
export CFLAGS="-I/usr/local/include -I/usr/local/Cellar/readline/6.3.8/include -I/usr/local/opt/openssl/include"
export LDFLAGS="-L/usr/local/lib -L/usr/local/Cellar/readline/6.3.8/lib -L/usr/local/opt/openssl/lib"
```

I then changed lua-tg.c and commented the following lines (664-666):
```c
static inline tgl_peer_t *get_peer (const char *s) { 
  return tgl_peer_get_by_name (TLS, s);
}
```

Compiled with:
```bash
./configure && make
```
