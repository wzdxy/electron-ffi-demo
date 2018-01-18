## Quick Start

```bash
# If your electron version is not v1.8.1 ,
# Change the target version in rebuild-ffi script package.json to your electron version before rebuild-ffi
npm i
npm run rebuild-ffi
npm run start
```

## Build

- Use electron-builder to Build
- Add Config:
    ```js
        "extraFiles": [
            "dll"               // Where *.dll File
        ]
    ```

## `MyDLL.dll` Source Code

- cpp

```cpp
#include "stdafx.h"
#include "testdll.h"
#include <iostream>
using namespace std;
float Add(float plus1, float plus2)
{
	int add_result = plus1 + plus2;
	return add_result;
}

char *Hello()
{
	return "Hello This is Cpp Addon";
}

int StrLength(char * str)
{
	return strlen(str);
}
```

- h
```h
#pragma once
#ifndef TestDll_H_
#define TestDll_H_
#ifdef MYLIBDLL
#define MYLIBDLL extern "C" _declspec(dllimport) 
#else
#define MYLIBDLL extern "C" _declspec(dllexport) 
#endif
MYLIBDLL char* Hello();
MYLIBDLL float Add(float plus1, float plus2);
MYLIBDLL int StrLength(char * str);
//You can also write like this:
//extern "C" {
//_declspec(dllexport) int Add(int plus1, int plus2);
//};
#endif
```


- def

```def
LIBRARY "MyDLL"
EXPORTS
Add @1
```
