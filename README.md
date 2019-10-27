
# MrLoop

Event loop for C using [io_uring](https://github.com/axboe/liburing) which requires linux kernel 5.3+

# Build

```
./bld
sudo ./bld install
```

# Benchmarks

Echo server benchmarked with https://github.com/haraldh/rust_echo_bench

```
Echo server ( examples/echo_server.c )

  mrloop    288,169 responses/sec
  epoll     191,011 responses/sec 

```

# Usage

A simple timer.  See more code in examples/

```
#include "mrloop.h"

static mrLoop *loop = NULL;

void on_timer() { 
  printf("tick\n");
}

static void sig_handler(const int sig) {
  printf("Signal handled: %s.\n", strsignal(sig));
  exit(EXIT_SUCCESS);
}

int main() {

  loop = createLoop(sig_handler);
  addTimer(loop, 1, on_timer);
  runLoop(loop);
  freeLoop(loop);

}
```