## APUE2: Rewrite mycat.c

> `mycat.c` implements a function that get the input string and output it.

# Origin version in C

```
#include "apue.h"

#define	BUFFSIZE	4096

int
main(void)
{
	int		n;
	char	buf[BUFFSIZE];

	while ((n = read(STDIN_FILENO, buf, BUFFSIZE)) > 0)
		if (write(STDOUT_FILENO, buf, n) != n)
			err_sys("write error");

	if (n < 0)
		err_sys("read error");

	exit(0);
}

```

# My version in CPP

```
#include <iostream>

int main(void) {
  std::string in;
  while (std::getline(std::cin, in)) {
    std::cout << in << std::endl;
  }

  exit(0);
}

```

