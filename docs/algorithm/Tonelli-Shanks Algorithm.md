---
layout: default
title: Tonelli-Shanks Algorithm
grand_parent: crypto
parent: algorithm
nav_order: 1
permalink: '4'
---

# Tonelli-Shanks Algorithm
{: .no_toc }

토넬리-샹크스 알고리즘

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Tonelli-Shanks Algorithm
토넬리-샹크스 알고리즘(Tonelli-Shanks Algorithm)은 모듈러 제곱근(modular square root)을 계산하는데 효율적인 알고리즘이다.
\\(x^2 \equiv a \pmod p\\)에서 \\(x\\)를 찾는 문제를 해결하는데 유용하게 사용된다.
여기서 \\(p\\)는 홀수 소수이고, \\(a\\)는 \\(p\\)의 제곱 잉여(quadratic residue)이다.

{: .note-title }
> 제곱 잉여(이차 잉여, quadratic residue)
>
> 수론에서 정수 \\(n\\)에 대하여, \\(a\\)가 \\(n\\)의 제곱 잉여라는 것은 \\(x^2 = a \bmod n\\)을 만족하는 정수 \\(x\\)가 존재한다는 것이다.

ECC, RSA 또는 이산 로그 문제를 해결하는 상황에서 모듈러 제곱근을 계산해야할 때 활용된다.

효율적이고 간단한 알고리즘이면서 \\(p-1\\)의 특정 분해 형태를 활용하여 계산 속도를 최적화한다는 장점이 있다.
하지만 \\(p\\)는 반드시 홀수 소수여야 하며, 입력 \\(a\\)가 \\(p\\)에 대해 제곱 잉여임이 보장되야한다는 제약 역시 존재한다.

## Tonelli-Shanks의 작동 방식
1. 입력 조건 확인하기
    - \\(a^{(p-1)/2} \bmod p = 1\\)인지 확인한다.
    - 만약 \\(a^{(p-1)/2} \bmod p \neq 1\\)이면, \\(a\\)는 제곱 잉여가 아니고 해가 존재하지 않는다.

2. \\(p-1\\)의 형태 분해하기
    - \\(p-1 = q \cdot 2^s\\)형태로 분해한다.
    - \\(q\\)는 홀수이고, \\(s\\)는 양의 정수이다.

3. 무작위 비제곱잉여(\\(z\\)) 찾기
    - \\(z\\)를 \\(p\\)에 대한 제곱 비잉여로 설정한다.
    - 즉, \\(z^{(p-1)/2} \bmod p = -1\\)

4. 초기값 설정하기
    - \\(c = z^q \bmod p\\)
    - \\(t = a^q \bmod p\\)
    - \\(r = a^{(q+1)/2} \bmod p\\)

5. 반복 계산
    - \\(t = r^2 \bmod p\\)가 1이 될 때까지 반복한다.
    - \\(t\\)를 업데이트 하면서 \\(c\\)와 \\(r\\) 값을 갱신한다.

6. 결과 반환
    - \\(x = r\\)는 해 중 하나이다. 다른 해는 \\(x' = p - r\\)로 표현된다.

## Tonelli-Shanks의 시간 복잡도
Tonelli-Shanks 알고리즘은 \\(O(log^2\,p)\\)의 시간 복잡도를 가진다.
이에 일반적인 탐색 방법보다 훨씬 더 효율적이다.

## Tonelli-Shanks의 코드
```python
def tonelli_shanks(a, p):
    # Step 1. 제곱잉여 확인하기
    if pow(a, (p - 1) // 2, p) != 1:
        raise ValueError("a is not a quadratic residue modulo p")

    # Step 2. p-1 = q * 2^s 형태로 분해하기
    s = 0
    q = p - 1
    while q % 2 == 0:
        q //= 2
        s += 1

    # Step 3. 제곱 비잉여 z 찾기
    z = 2
    while pow(z, (p - 1) // 2, p) != p - 1:
        z += 1

    # Step 4. 초기화
    c = pow(z, q, p)
    t = pow(a, q, p)
    r = pow(a, (q + 1) // 2, p)
    m = s

    # Step 5. 반복하여 해 찾기
    while t != 1:
        t2i = t
        i = 0
        while t2i != 1:
            t2i = pow(t2i, 2, p)
            i += 1
        b = pow(c, 2 ** (m - i - 1), p)
        m = i
        c = pow(b, 2, p)
        t = (t * c) % p
        r = (r * b) % p

    # Step 6. 첫 번째 해 r과 두 번째 해 p-r 반환
    return r, p - r


p = 13  # 소수
a = 10  # 제곱잉여
try:
    x1, x2 = tonelli_shanks(a, p)
    print(f"Solutions: x1 = {x1}, x2 = {x2}")
except ValueError as e:
    print(e)
```