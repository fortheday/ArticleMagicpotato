# strncpy()와 strncpy_s()에 대한 오해 + snprintf_s() 버그 (_TRUNCATE) 
* 2008-04-01. magicpotato.  

```
strncpy()는 복사되었으면 하는 문자열의 길이를 넘어서지 않게 복사해 준다. 
그리고 대상 버퍼를 넘어서게 되면 NULL로 끝나지 않는 문자열까지 복사하게 된다. 예를 들면 아래와 같다. 

strncpy(dest, 8, "1234567"); // dest == { '1', '2', '3', '4', '5', '6', '7', NULL } 
strncpy(dest, 8, "12345678"); // dest == { '1', '2', '3', '4', '5', '6', '7', '8' } 


strncpy_s() 는 대상 버퍼가 실제 수용가능한 크기와 복사되었으면 하는 문자열의 길이 두가지를 넘긴다. 
strncpy()와 strncpy_s()의 다른점이 있다면 strncpy_s()는 '복사 되었으면 하는 문자열의 길이'를 넘어서서 복사를 할 때 마지막을 항상 NULL로 끝나게 해준다는 점이다. 

다음과 같은 코드는 런타임 에러를 발생시킨다. 

// 이 코드는 buf에 1, 2, 3, 4, 5, 6, 7, 8, NULL .. 총 9개의 문자열을 넣으려다가 에러가 나게 된다. 
char dest[8]; 
strncpy_s(buf, _countof(buf), "123456789000", _countof(buf)); 


따라서 strncpy_s()를 사용할 때는 버퍼 크기와, 복사하고 싶은 길이를 다르게 주어야 한다. 

char dest[8]; 
strncpy_s(buf, _countof(buf), "123456789000", _countof(buf)-1); 



참고. 

strcpy_s()를 사용하면 버퍼 크기를 넘어서는 데이터를 넘을 때 
자동으로 막아준다고 착각하는 경우가 있다. (strncpy처럼) 

strcpy_s()에 넘기는 2번째 인자인 dest_size는 '내가 이 정도까지만 복사하고싶다'의 의미가 아니라 
'여기 지정한 크기를 넘어서 복사하려고 하면 프로그램을 멈추고 에러창을 띄워라' 의 의미로 보아야 한다. 

// 이 코드는 이쁘게 dest에 1234567까지만 복사해 주는 것이 아닌, 프로그램을 뻗게 하는 코드다. 
char dest[8]; 
strcpy_s(dest, _countof(dest), "123456789"); 


연장해서 sprintf_s() 와 _snprintf_s() 에도 똑같이 적용된다. 

sprintf_s(buf, _countof(buf), "%s 1234567", "1212"); // 프로그램 오류를 내는 코드 
_snprintf_s(buf, _countof(buf), _countof(buf), "123456789%d", 121212); // strncpy_s()와 같은 이유로 오류를 내는 코드 
_snprintf_s(buf, _countof(buf), _countof(buf)-1, "1234567%d", 121212); // 정상적으로 작동하며, 이렇게 써야 하는 코드 



* gpg의 비회원님의 내용 추가 - 보충 감사드립니다. 

strncpy_s(), _snprintf_s() 함수의 복사하고 싶은 길이(size_t count)에 _TRUNCATE 를 넣으면 
수용가능한 버퍼 크기(size_t sizeOfBuffer)에 지정한 값 -1 을 넣은것과 같게 동작한다. 

다음 두개의 코드는 결과가 같다. 
strncpy_s(buf, _countof(buf), "123456789000", _countof(buf)-1); 
strncpy_s(buf, _countof(buf), "123456789000", _TRUNCATE); 


** _TRUNCATE와 관련한 버그 안내 (2008-04-02, VS2005 VC8.0.50727.762 - SP.050727.7600 기준) 

다음 프로토타입을 갖는 함수에는 count에 _TRUNCATE를 사용해도 된다. 
int _snprintf_s( char *buffer, size_t sizeOfBuffer, size_t count, const char *format [, argument] ... );  

다음 프로토타입을 갖는 함수의 count에 _TRUNCATE를 사용하면 스택이 깨진다. 
template <size_t> int _snprintf_s( char (&buffer)[size], size_t count, const char *format [, argument] ... ); // C++ only  

템플릿버전에서는 내부적으로 매크로를 사용하고 있는데 sizeOfBuffer와 count값 두가지가 모두 -1 로 넘어가면서 코드 내부적으로 buffer[(size_t)-1] = NULL; 이라는 코드를 실행하면서 잘못된 메모리를 쓰게 된다. 



** 티벳의 독립을 지지하는 아이스닥님이 알려주신 버그 수정법 

CRTDEFS.h 파일 열어서 
모든 _Size를 _SUCKS_MS_BUG_Size 등 다른 이름으로 수정하면 된다. (원작자 표현 존중) 

다만, 자기 컴퓨터의 버그만 고쳐지는 것이므로 되도록 혼자 작업하는게 아니라면 우회해서 사용하는것이 좋겠다. 


- 버그내용 설명 
stdio.h의 매크로 선언부와 crtdefs.h의 매크로 내용 정의부의 인자이름 _Size가 서로 겹쳐서 발생하는 버그라고 한다. 

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
