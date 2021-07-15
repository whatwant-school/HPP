# HPP
High Performance Python - 2nd

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

</div>
</details>


### 추가 공부하면 좋을 내용
- GIL (Global interpreter Lock)
  - Python은 왜 GIL 정책을 적용했을까?
