---
title: "c 언어"
excerpt: "선택 정렬 알고리즘"
toc: true
toc_sticky: true
toc_label: "목차"
categories:
  - c
tags:
  - 선택정렬
  - c
last_modified_at: 2023-02-27T17:51:00-05:00
---

## 1. 선택 정렬 알고리즘

선택정렬 알고리즘(selection sort)을 한마디로 정의하자면 제일 처음 0번째 배열 부터 다음 배열까지 하나하나 채워나가는 방식이라고 할 수 있다.  
백문이 불여일견! 우선 코드를 보자.

## 2. 예제 코드

```c
#include <stdio.h>
#include <string.h>
#define LENGTH sizeof(city) / sizeof(city[0])

int main() {

	char city[][10] = { "seoul", "daejeon", "daegu", "kwangju", "incheon", "jeju", "busan" };
	char temp[10] = " ";
	int i = 0, j = 0, idx = 0;

	printf("=== 정렬하기 전 ===\n");
	for (i = 0; i < LENGTH; i++) {
		printf("%s ", city[i]);
	}
	printf("\n\n");

	for (i = 0; i < LENGTH - 1; i++) {
		idx = i;
		printf("비교 기준 문자열 인덱스 : %d\n", idx);
		for (j = i + 1; j < LENGTH; j++) {
			printf("기준 문자열과 비교할 인덱스 : %d\n", j);
			if (strcmp(city[idx], city[j]) > 0) {
				printf("%s는 %s보다 아스키 코드가 크므로 기준 문자열 인덱스 %d를 %d로 변경\n", city[idx], city[j], idx, j);
				idx = j;
			}
			strcpy_s(temp, sizeof(temp), city[i]);
			strcpy_s(city[i], sizeof(temp), city[idx]);
			strcpy_s(city[idx], sizeof(temp), temp);

			for (int k = 0; k < LENGTH; k++) {
				printf("%s ", city[k]);
			}
			printf("\n");
		}

	}

	printf("=== 정렬하기 후 ===\n");
	for (i = 0; i < LENGTH; i++) {
		printf("%s ", city[i]);
	}
	printf("\n\n");


	return 0;
}
```

## 3. 설명

처음엔 배열의 첫번째 문자열인 "seoul"이 비교 기준 문자열이 돼서 두번째 문자열인 "daejeon" 부터 마지막 문자열인 "busan" 까지 내부 for문을 돌면서, strcmp()를 통해 문자열의 문자를 하나씩 비교해 기준 문자열이 크면 1을 리턴하고 작으면 -1을 리턴한다.

결국 내부 for문을 한바퀴 돌게되면 문자 'b'로 시작하는 "busan"이 첫번째 문자열에 오게 된다. 다시 외부 for문을 통해 두번쨰 문자열인 "daejeon"이 비교 기준 문자열이 되고 내부 for문을 돌게 된다.

## 4. 시간 복잡도

처음 기준 문자열 "seoul"이 세팅되고 내부 for문을 통해 n-1(LENGTH-1)번 실행되고 두번째 문자열 "daejeon"이 내부 for문을 통해 n-2번 실행된다.

시행 횟수는 n-1 + n-2 + ... + 2 + 1 이라서 총 $\frac{(n-1)(n-2)}{2}$ 회 시행되고 빅오 표기법(Big-O Notation)으로 O($n^2$)이라 효율적인 방법은 아니다.
