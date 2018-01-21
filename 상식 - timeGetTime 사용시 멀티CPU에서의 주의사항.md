#  timeGetTime 사용시 멀티CPU에서의 주의사항
* 2018-01-21. magicpotato.

`timeGetTime()`, `QueryPerformanceFrequency()` 함수를 멀티CPU에서 사용할 때 값이 튀는 문제가 있을 수 있다. 물리적인 CPU가 2개 이상 장착된 PC에서는 주의해야 한다. 해결방법은 `SetThreadAffinityMask()`를 통해 대상 함수를 사용해 시간을 처리하는 쓰레드는 한 개의 CPU만 사용하도록 고정시키면 된다.

[참고문서](https://msdn.microsoft.com/en-us/library/ee417693.aspx)