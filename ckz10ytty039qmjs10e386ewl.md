## APUE1: Rewrite ls1.c in CPP

> `ls1.c` implements a function that can list the files under a directory, and I rewrite it using CPP.

# Origin version in C

```C
#include "apue.h"
#include <dirent.h>

int
main(int argc, char *argv[])
{
	DIR				*dp;
	struct dirent	*dirp;

	if (argc != 2)
		err_quit("usage: ls directory_name");

	if ((dp = opendir(argv[1])) == NULL)
		err_sys("can't open %s", argv[1]);
	while ((dirp = readdir(dp)) != NULL)
		printf("%s\n", dirp->d_name);

	closedir(dp);
	exit(0);
}

```

# My version in CPP

```CPP
#include <filesystem>
#include <iostream>
namespace fs = std::filesystem;

int main(int argc, char *argv[]) {
  if (argc != 2) {
    std::cout << "usage: ls directory_name" << std::endl;
    exit(0);
  }

  std::string path = argv[1];
  if (!fs::exists(path)) {
    std::cout << "can't open " << path << std::endl;
    exit(0);
  }

  for (const auto &entry : fs::directory_iterator(path)) {
    std::cout << entry.path().filename().string() << std::endl;
  }
  exit(0);
}
```
