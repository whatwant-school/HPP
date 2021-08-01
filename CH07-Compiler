# Chapter 07 - C 언어로 컴파일하기


## kind of compiler

### Cython(사이썬)
- C-Extensions for Python
- C 언어로 컴파일하기 위해 사용하는 가장 일반적인 도구
- Numpy와 일반 파이썬 코드를 모두 커버(단, C 언어를 어느 정도 이해해야 함)
- https://cython.org/

### Numba
- Numba translates Python functions to optimized machine code at runtime using the industry-standard LLVM compiler library.
- numpy 코드에 특화된 새로운 컴파일러
- http://numba.pydata.org/

### PyPy
- replacement for CPython. It is built using the RPython language that was co-developed with it.
- 일반 파이썬 실행환경을 대체하는 非 numpy 코드를 위한 JIT 컴파일러
- https://www.pypy.org/


## compile을 통한 속도 개선

### calculate vs. others
- 같은 연산을 무수히 반복하는 코드가 많은 수학적인 연산에서 속도 개선 효과(임시 객체를 많이 사용하기 때문?)
- 입출력 관련 코드, 외부 라이브러리(정규 표현식, 문자열 연산, DB 라이브러리 호출) 등에서는 효과 없음

### numpy vs. others
- numpy 연산은 임시 객체를 많이 사용하지 않으므로 효과 없음
- Python 코드이고 대부분의 코드가 루프일 때 속도 개선 효과
