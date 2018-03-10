# ANTLR, 파서 제네레이터 개념 요약
* 2018-03-10. magicpotato

> ANTLR(무식), 회사업무때문에 공부하는 중이므로 한정적, 구체적 개념으로 공부내용을 정리. 이 이상은 나도 모름 ㅜ

![](http://dalkescientific.com/writings/diary/antlr_gui_mw.png)

## Antlr 소개 (ANother Tool for Language Recognition) [ANTLR](http://www.antlr.org/)
   1. 파서 제네레이터
   1. 구조화된 텍스트/바이너리를 읽고, 처리하고, 실행하거나 번역(컴파일)하는데 사용
   1. 언어(데이터 정의언어, 프로그래밍 언어 등 어떤거든), 툴, 프레임워크를 만드는데 사용 (만든다가 아니라 만드는데 사용)
   1. ANTLR은 파서를 생성한다: (그 파서는 파스 트리를 만들고 순회?할 수 있다)
   1. Predicated-LL(k) 파서 (?)
   1. Lex, Yacc 대체
   1. 오픈소스, Java로 만듦
   1. ANTLR로 입력: .g (문법파일)
   1. ANTLR의 출력: .java (토크나이저 + 파스트리 출력기?)
   1. 프로그래밍 언어에 한정되는 툴이 아니다.

> ANTLR (ANother Tool for Language Recognition) is a powerful parser generator for reading, processing, executing, or translating structured text or binary files. It's widely **used** to build languages, tools, and frameworks. From a grammar, **ANTLR generates a parser** that can build and walk **parse trees**.


## 컴파일러 개발 자동화 도구의 필요성

C언어를 x86, Arm용 실행파일로 만드려면 2개의 컴파일러가 필요하다. N개의 프로그래밍 언어를 M개의 플랫폼에서 컴파일 하려면 NM개가 필요하다. 이 작업을 효율적으로 하기 위한 도구가 **컴파일러 자동화 도구**이다. 이런 도구들을 Compiler Generator, Compiler Compiler 라고 부른다. 기본적으로는 Input:Output이 N:M 개념일 때 사용하기 위한 툴 같다.


1. 컴파일러 처리 과정 요약
   1. FrontEnd (프로그래밍 언어 처리)
      1. 어휘분석: 소스코드 스트림을 토큰 목록으로 추출
         `a = b + 1; ==> { a, =, b, +, 1, ; }`
      2. 구문분석: 토큰 목록을 파스 트리로 구축
         1. 계산기 만들 때 `1+2`를 해석하면 `+`가 루트노드, 우측자식이 `1`, 좌측자식이 `2`가 되는 그 트리
      3. 중간코드 생성
   2. BackEnd (목적 언어/코드 생성)
      1. 코드 최적화
      2. 목적 코드 생성


## Lex
   1. Tool.
   1. **어휘 분석기** 생성기 (Lexical Anlyzer Generator, Tokenizer Generator?)
   1. Lex로 입력: 토큰에 대한 정규표현식과 토큰 처리코드들
   1. Lex의 출력: 입력에서 받은 내용을 프로그래밍 해 놓은 분석기 (소스코드)
   1. Lex.generated.exe의 입력: 프로그래밍 언어 소스코드
   1. Lex.generated.exe의 출력: 토큰 목록

   > 아마도 Tokenizer의 핵심코드는 미리 짜여져 있고, 하드코딩 되는 일부 영역을 생성/치환(generate)해 주는것이라 추측.
   > 토큰 정의/처리코드를 동적으로 입력받아서 처리하는 동적처리기의 개념도 있긴 하겠지만, 제한 되기 때문에 생성기의 형태를 가져가는 것 같다.


## Yacc (Yet Another Compiler Compiler)
   1. Tool.
   1. 구분 문석기 생성기 (Syntax Analyzer)
   1. **파스 트리 생성기**의 생성기
   1. Yacc로 입력: 문법규칙(Syntax), 처리코드
   1. Yacc의 출력: 문법 규칙에 의해 처리하는 파스 트리 생성기 (소스코드)
   1. Yacc.generated.exe의 입력: 토큰 목록
   1. Yacc.generated.exe의 출력: 파스 트리


EOF
