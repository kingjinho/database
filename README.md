# database

## 데이터 베이스는 어떻게 작동하는가? 에 대한 프젝트입니다.
[Write a simple database](https://cstack.github.io/db_tutorial/)을 기반으로 작성하였습니다.

## Part 1.
- 기본적으로 데이터베이스는 두 파트로 나누어진다.
- 우리가 작성하는 쿼리를 받아 바이트코드로 변환하는 **front**,
- 프론트에서 바이트코드를 받아 db 파일에서의 실직적인 IO를 수행하는 **backend**.
- 즉, 데이터베이스의 작동방식을 한마디로 설명하면
    - 쿼리를 바이트코드로 만들어서(컴파일) 가상머신(vm)에서 실행시킨다 입니다.

- front와 backend를 좀 더 자세히 나눠보면 보면
    - front: Tokenizer, Parser, Code generator
    - backend: virtual machine, b-tree, pager, os interface

로 구성되어있는데, 각각의 단계에서 하는 일을 살펴보면

- front
    - tokenizer
        - 사용자가 작성한 쿼리(문장)를 토큰화(각각의 작은 단위로 나누는 작업)을 진행하고 parser에게 전달합니다.
        - 토큰을 전달할때 한번에 다 전달하는게 아닌, 하나씩 전달합니다.
    - parser
        - 전달받은 토큰들을 분석하여 각 토큰들의 의미와 관계를 설명하는 트리를 생성합니다.
    - code generator
        - parser에서 전달 받은 트리형태의 데이터를 기반으로 다시 한번 분석하고 바이트 코드를 생성합니다. 
---
- backend
    - virtual machine
    - b-tree
    - pager
    - os interface

- 두 파트로 나누었을때의 장점
    - 복잡성 제거 - vm은 syntax 에러를 걱정할 필요가 없음
    - 공용으로 쓰는 쿼리를 캐싱하여 성능 향상
    