# strncpy와 strncpy_s에 대한 오해 및 snprintf_s _TRUNCATE 버그
* 2008-04-01. magicpotato.
* 2018-01-22 update.

# strncpy()

`strncpy()`는 지정한 길이를 넘지 않게 복사해 준다. 주의할 점은 다음과 같다.

1. 최대길이보다 크게 복사할 경우 `Dest[_Count-1]` 은 `NULL`이 대입되지 않는다.

```cpp
// 원형
char * strncpy(char *_Destination, char const *_Source, size_t _Count);

// 예시
char buf[4];
strncpy(buf, 4, "123");  // buf == { '1', '2', '3', '\0' }
strncpy(buf, 4, "1234"); // buf == { '1', '2', '3', '4' }

```

# strncpy_s()

`strncpy_s()`는 두가지 길이값을 받는다. (1)목적 버퍼의 크기와 (2)복사할 길이. 주의할 점은 다음과 같다.

1. strncpy()와 달리 (2)복사할 길이가 넘쳐도 `Dest[_Count-1]`을 `NULL`로 대입해 준다.
2. 직전의 특성때문에 대상버퍼길이보다 복사길이가 같거나 크면 런타임 예외를 발생시킨다.

```cpp
// 원형
errno_t strncpy_s(  
   char *strDest,
   size_t numberOfElements,// (1)목적 버퍼의 크기
   const char *strSource,
   size_t count);          // (2)복사할 길이

// 예시
char buf[4];
strncpy_s(buf, _countof(buf), "12345", _countof(buf)); // buf == { '1', '2', '3', '4', '\0' }
```

위와 같은 코드는 총 5개의 문자를 복사하다가 런타임 예외를 발생시킨다. 그래서 아래와 같이 사용해야 한다.

```cpp
char buf[4];
strncpy_s(buf, _countof(buf), "12345", _countof(buf)-1); // buf == { '1', '2', '3', '\0' }
```

# strcpy_s()

`strcpy_s()`에 지정한 길이가 `strncpy()` 처럼 작동한다고 착각해서는 안된다. 인자로 넘기는 `numberOfElements`는 '이 길이까지 복사하고싶다'라는 뜻이 아니다. '이 길이를 넘어서면 런타임 에러를 발생시켜라' 라는 뜻이다.

```cpp
// 원형
errno_t strcpy_s(  
   char *strDestination,  
   size_t numberOfElements,  
   const char *strSource   
);  

// 예시
char buf[4];
strcpy_s(buf, _countof(buf), "12345"); // buf == { '1', '2', '3', '4', '5', '\0' }
```

# sprintf_s(), _snprintf_s()

위의 논리와 똑같다.

```cpp
char buf[4];
sprintf_s(buf, _countof(buf), "%s abc", "123"); // 런타임에러
_snprintf_s(buf, _countof(buf), _countof(buf), "12%d", 345); // 에러. strncpy_s()와 같은 이유.
_snprintf_s(buf, _countof(buf), _countof(buf)-1, "12%d", 345); // 정상. "123\0"이 복사된다.
```

# _TRUNCATE
> gpgstudy의 비회원님이 알려주신 내용

`strncpy_s()`, `_snprintf_s()` 함수에 복사할 길이(`count`) 값으로 `_TRUNCATE` 를 넘겨주면, 목적 버퍼의 크기(`numberOfElements`) 지정값 `-1`을 `count`에 넣은 것으로 동작한다. 다음 코드의 결과는 같다.

```cpp
strncpy_s(buf, _countof(buf), "12345", _countof(buf)-1); 
strncpy_s(buf, _countof(buf), "12345", _TRUNCATE); 
```

# _TRUNCATE 버그
> (2008-04-02, VS2005 VC8.0.50727.762 - SP.050727.7600 기준)

다음 프로토타입을 갖는 함수에는 count에 _TRUNCATE를 사용해도 된다.
```
int _snprintf_s( char *buffer, size_t sizeOfBuffer, size_t count, const char *format [, argument] ... );  
```

다음 프로토타입을 갖는 함수의 count에 _TRUNCATE를 사용하면 스택이 깨진다. 
```
template <size_t> int _snprintf_s( char (&buffer)[size], size_t count, const char *format [, argument] ... );
```

템플릿버전 내부에서 사용하는 매크로와 관련하여 sizeOfBuffer, count 값이 모두 -1로 처리되면서 `buffer[(size_t)-1] = NULL` 코드를 실행하게 된다.

**티벳의 독립을 지지하는 아이스닥**님이 알려주신 버그 수정법 (원작자 표현 그대로 인용)
```
CRTDEFS.h 파일 열어서 모든 _Size를 _SUCKS_MS_BUG_Size 등 다른 이름으로 수정하면 됩니다.
```

수정한 사람이 사용하는 PC의 버그만 고쳐지는 것이므로 팀작업을 한다면 그냥 쓰지 말자.

## _TRUNCATE 버그 설명

stdio.h의 매크로 선언부와 crtdefs.h의 매크로 내용 정의부의 인자이름 _Size가 서로 겹쳐서 발생하는 버그라고 한다. 

```cpp
[stdio.h] 
__DEFINE_CPP_OVERLOAD_SECURE_FUNC_0_2_ARGLIST(int, _snprintf_s, _vsnprintf_s, __out_bcount(_Size) char, _Dest, __in size_t, _Size, __in_z __format_string const char *,_Format) 

[crtdefs.h] 
#define __DEFINE_CPP_OVERLOAD_SECURE_FUNC_0_2_ARGLIST(_ReturnType, _FuncName, _VFuncName, _DstType, _Dst, _TType1, _TArg1, _TType2, _TArg2) \ 
    extern "C++" \ 
    { \ 
        __pragma(warning(push)); \ 
        __pragma(warning(disable: 4793)); \ 
    template <size_t _Size> \ 
    inline \ 
    _ReturnType __CRTDECL _FuncName(_DstType (&_Dst)[_Size], _TType1 _TArg1, _TType2 _TArg2, ...) \ 
    { \ 
        va_list _ArgList; \ 
        _crt_va_start(_ArgList, _TArg2); \ 
        return _VFuncName(_Dst, _Size, _TArg1, _TArg2, _ArgList); \ 
```

EOF
