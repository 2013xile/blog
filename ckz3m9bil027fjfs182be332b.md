## APUE4: Rewrite hole.c

`hole.c` implements a function that create a file and write.

# Origin version in C

```
#include "apue.h"
#include <fcntl.h>

char	buf1[] = "abcdefghij";
char	buf2[] = "ABCDEFGHIJ";

int
main(void)
{
	int		fd;

	if ((fd = creat("file.hole", FILE_MODE)) < 0)
		err_sys("creat error");

	if (write(fd, buf1, 10) != 10)
		err_sys("buf1 write error");
	/* offset now = 10 */

	if (lseek(fd, 16384, SEEK_SET) == -1)
		err_sys("lseek error");
	/* offset now = 16384 */

	if (write(fd, buf2, 10) != 10)
		err_sys("buf2 write error");
	/* offset now = 16394 */

	exit(0);
}
```

# My version in CPP

```
#include <fstream>
#include <iostream>

int main() {
  std::string str1 = "abcdefghij";
  std::string str2 = "ABCDEFGHIJ";

  std::ofstream outfile;
  outfile.open("file.hole");
  outfile << str1;

  outfile.seekp(16384);

  outfile << str2;
  outfile.close();
  exit(0);
}
```