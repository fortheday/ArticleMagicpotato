# GetLastError()의 반환값을 OS에 정의된 문자열로 변환

```cpp
int nError = GetLastError();

char buf[1024];

FormatMessage(FORMAT_MESSAGE_FROM_SYSTEM | FORMAT_MESSAGE_IGNORE_INSERTS, NULL, 10053, 0, buf, 1024, NULL);

MessageBox(NULL, buf, NULL, MB_OK);
```

EOF
