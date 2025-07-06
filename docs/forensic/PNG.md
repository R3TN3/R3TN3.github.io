---
title: PNG 파일 시그니처
parent: Forensic
nav_order: 2
---

# PNG File Signatures
{: .no_toc }

PNG 파일 시그니처

## contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## PNG 파일 시그니처(File Signatures)
크기가 1x1 픽셀인 png 파일을 만들어 png 파일의 파일 시그니처를 확인한다.

{% include lazyload.html image_src= https://github.com/R3TN3/R3TN3.github.io/blob/main/docs/forensic/img/1x1png.png %}



{: .note-title }
> PNG 파일 시그니처
>
> Header Signature(Hex)        (8Bytes)
> 89 50 4E 47 0D 0A 1A 0A        (89 50 4E -> PNG )
>
> Footer Signature(Hex)        (8Bytes)
> 49 45 4E 44 AE 42 60 82

그러면 다음과 같이 8bytes로 구성된 헤더와 푸터의 시그니처를 확인할 수 있다.

