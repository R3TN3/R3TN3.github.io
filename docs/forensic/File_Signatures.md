---
title: 파일 시그니처(File Signatures)
parent: Forensic
nav_order: 1
---

# File Signatures
{: .no_toc }

파일 시그니처

## contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 파일 시그니처(File Signatures)

파일을 담고 있는 데이터를 유용하게 사용하기 위해서는 관련된 소프트웨어가 필요하다.
소프트웨어들은 각각 자신만의 고유한 파일 포맷을 만들어 사용한다.
따라서 파일들의 고유한 포맷을 통해 소프트웨어가 파일을 해석한다.

시그니처는 보통 헤더(Header), 푸터(Footer)로 구성된다.

## 파일 시그니처 모음

| Length | Header Signature(Hex)    | Footer Signature(Hex)     | File Type | Description |
| :------ | :--------------------------- | :-------------------------  | :--------- | :----------- |
| 8       | 89 50 4E 47 0D 0A 1A 0A | 49 45 4E 44 AE 42 60 82 | PNG       |               |

