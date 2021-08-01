# HPP
High Performance Python - 2nd

- https://github.com/mynameisfiber/high_performance_python_2e

---
## CHAPTER 01 - 고성능 파이썬 이해하기

<details>
<summary>접기/펼치기 버튼</summary>
<div markdown="1"><BR />

### 이상적인 컴퓨팅

```python
import math


def check_prime(number):
    sqrt_number = math.sqrt(number)
    for i in range(2, int(sqrt_number) + 1):
        if (number / i).is_integer():
            return False
    return True


print(f"check_prime(10,000,000) = {check_prime(10_000_000)}")
print(f"check_prime(10,000,019) = {check_prime(10_000_019)}")
```
```bash
check_prime(10,000,000) = False
check_prime(10,000,019) = True
```

- 위의 코드를 CPU의 벡터화 연산을 이용하도록 작성한다고 하면...

```python
import math


def check_prime(number):
    sqrt_number = math.sqrt(number)
    numbers = range(2, int(sqrt_number) + 1)
    for i in range(0, len(numbers), 5):
        result = (number / numbers[i:(i + 5)]).is_integer()
        if any(result):
            return False
    return True


print(f"check_prime(10,000,000) = {check_prime(10_000_000)}")
print(f"check_prime(10,000,019) = {check_prime(10_000_019)}")
```

- 한 번에 5개씩 처리하는 벡터화 코드 ... 다만, 위의 코드는 동작하는 코드는 아니다.



### 파이썬의 가상 머신

```python
import timeit


def search_fast(haystack, needle):
    for item in haystack:
        if item == needle:
            return True
    return False


def search_slow(haystack, needle):
    return_value = False
    for item in haystack:
        if item == needle:
            return_value = True
    return return_value


if __name__ == "__main__":
    iterations = 10000
    haystack = list(range(1000))
    setup = "from __main__ import (haystack, needle, search_fast, search_slow)"

    needle = 5
    print(
        f"Testing search speed with {len(haystack)} items and needle close to the head of the list"
    )

    t = timeit.timeit(
        stmt="search_fast(haystack, needle)", setup=setup, number=iterations
    )
    print(f"search_fast time: {t/iterations:.5e}")

    t = timeit.timeit(
        stmt="search_slow(haystack, needle)", setup=setup, number=iterations
    )
    print(f"search_slow time: {t/iterations:.5e}")
```
```bash
Testing search speed with 1000 items and needle close to the head of the list
search_fast time: 9.84165e-07
search_slow time: 1.73868e-04
```

- 2가지 방식 모두 `O(n)` 복잡도를 갖지만, 중간에 빠져나오도록 하는 방식이 당연히 빠르다


### 모범적 작업 절차

- 문서화
- 좋은 구조
- 테스트


### 주피터 노트북 잘 다루기

- assert
- Exception - ValueError
- nbdime (https://nbdime.readthedocs.io/)

    
### 추가 공부하면 좋을 내용
- GIL (Global interpreter Lock)
  - Python은 왜 GIL 정책을 적용했을까?
  - https://www.artima.com/weblogs/viewpost.jsp?thread=214235

</div>
</details>


---
## CHAPTER 02 - 

<details>
<summary>접기/펼치기 버튼</summary>
<div markdown="1"><BR />

### magic function
- https://ipython.readthedocs.io/en/stable/interactive/magics.html


### functools.wraps
- https://velog.io/@doondoony/python-functools-wraps


### 여러가지 Visualize tools
- https://stackoverflow.com/questions/4544784/how-can-you-get-the-call-tree-with-python-profilers

</div>
</details>


---
## CHAPTER 03 - 

<details>
<summary>접기/펼치기 버튼</summary>
<div markdown="1"><BR />

### bisect
- https://velog.io/@gojaegaebal/201223-개발일지16일차-파이썬에서-bisect-함수-활용-feat.백준-8983번


### Python dictionary implementation
- https://uiandwe.tistory.com/1262


### The working principle of functions and generators in python
- https://www.fatalerrors.org/a/the-working-principle-of-functions-and-generators-in-python.html

</div>
</details>


---
## CHAPTER 04 - 

<details>
<summary>접기/펼치기 버튼</summary>
<div markdown="1"><BR />

### What's the future of the pandas library?
- https://www.dataschool.io/future-of-pandas/


### map vs. apply
- 일반적으로 map은 python native(그러니까, 판다스가 아닌 그냥 python)에서 functional programming의 원형을 수행하는 역할을 제공합니다.
- python의 iterable 객체(그러니가 list와 같이 여러개의 값을 순차적으로 접근하는 객체)에 map()내에 기술된 함수를 적용하면 해당 함수를 iterable 객체의 개별 값을 입력해주면서 반환값을 다시 iterable 객체로 저장할 수 있게 해줍니다(요약하자면 반복적으로 함수를 호출할 시에 for loop를 쓸 필요가 없게 해줍니다).
- apply도 map과 유사한 역할을 합니다. 단 apply는 pandas에서 사용되며 python native에서는 사용하지 않습니다(즉 DataFrame/Series에만 적용되고 list에는 적용되지 않습니다).
- 그리고 pandas도 map이 있지만 apply가 워낙 강력해서 잘 사용하지 않습니다.


### pandas on Spark
- https://koalas.readthedocs.io/en/latest/


</div>
</details>
