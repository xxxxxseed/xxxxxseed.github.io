---
title: "c 언어"
excerpt: "선택 정렬 알고리즘"

categories:
  - c
tags:
  - 선택정렬
  - c
last_modified_at: 2023-02-27T17:51:00-05:00
---

선택정렬 알고리즘(selection sort)을 한마디로 정의하자면 제일 처음 0번째 배열 부터 다음 배열까지 하나하나 채워나가는 방식이라고 할 수 있다.  
백문이 불여일견! 우선 코드를 보자.

```c
#include <stdio.h>
#include <string.h>
#define LENGTH sizeof(city) / sizeof(city[0])

int main() {

	char city[][10] = { "seoul", "daejeon", "daegu", "kwangju", "inchon", "jeju", "busan" };
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