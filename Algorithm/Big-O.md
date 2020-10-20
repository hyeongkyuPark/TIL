# Big-O(빅오) 표기법

## 🕝 시간복잡도
- 시간복잡도란 알고리즘이 문제를 해결하기 위한 시간(연산)의 횟수를 의미
- 알고리즘을 평가하는데 있어 수행시간과 메모리 사용량을 평가기준으로 두는데 수행시간에 해당하는 것이 `시간복잡도(Time Complexity)`, 메모리 사용량에 해당하는 것이 `공간복잡도(Space Complexity)`
- 연산 횟수를 카운팅 할때 3가지 경우
    - 최선의 경우(Best Case)
    - 최악의 경우(Worst Case)
    - 평균적인 경우(Average Case)
- 기본적으로 최악의 경우로 알고리즘의 성능을 파악(Big-O 표기법)


## ⭕️ 빅오 표기법
- 알고리즘 최악의 경우 복잡도
    - O(1) : 상수 시간
    - O(n) : 선형 시간
    - O(n<sup>a</sup>) : a차 시간
    - O(log n) : 로그 시간

## ⚖️ 빅오 법칙
- 계수 법칙 : 입력 크기 n과 관련되지 않은 계수를 제거. n이 무한에 가까워지는 경우 다른 계수는 무시해도 되기 때문  
    ```
    f(5n) = f(n), f(n+2) = f(n)
    ```
    - **예시 CODE 💻**  
    ``` javascript
    function a(n) {
        var count = 0;

        for(var i=0; i<5*n; i++) {
            count += 1;
        }

        return count;
    }
    ```
    - **코드 풀이 📝**  
        - 위의 코드는 f(n) = 5n(0부터 5n까지 실행하기 때문) 이지만, n이 무한대 또는 아주 큰 수에 가까워질 때 네 개의 연산이 추가적으로 존재한다고 해서 달라지는 것은 없기 때문에 빅오 표기법에서 계수 법칙에 의해 모든 상수는 무시
- 합의 법칙 : 시간 복잡도를 더할 수 있음
    ```
    f(4n) + f(n) = f(5n)
    ```
    - **예시 CODE 💻**  
    ``` javascript
    function a(n) {
        var count = 0;

        for(var i=0; i<5*n; i++) {
            count += 1;
        }

        for(var i=0; i<n; i++) {
            count += 1;
        }

        return count;
    }
    ```
    - **코드 풀이 📝**  
        - 위의 코드는 f(n) = 5n 과 f(n) = n 을 가지고 있으므로 결과값은 합의 법칙(각 루프의 시간 복잡도는 개별적으로 계산된 다음 더해저야 함)에 의해 6n이 됨
- 곱의 법칙 : 중첩 반복문에서 곱의 법칙이 적용
    ```
    f(4n)*f(n) = f(4n²)
    ```
    - **예시 CODE 💻**  
    ``` javascript
    function a(n) {
        var count = 0;

        for(var i=0; i<n; i++) {
            count += 1;
            for(var j=0; j<5*n; j++) {
                count += 1;
            }
        }

        return count;
    }
    ```
    - **코드 풀이 📝**  
        - 위의 코드는 내부 루프에 의해 5n번 실행 되고 내부 루프가 외부 루프에 의해 n번 실행되기 때문에 곱에 법칙을 따라 f(n) = 5n*n = 5n² 이 됨
- 다항 법칙 : a차 시간 복잡도를 지닌 반복문에서 적용
    ```
    f(n*n) = f(n²)
    ```
    - **예시 CODE 💻**  
    ``` javascript
    function a(n) {
        var count = 0;

        for(var i=0; i<n*n; i++) {
            count += 1;
        }

        return count;
    }
    ```
    - **코드 풀이 📝**  
        - 위의 코드는 루프가 n*n번 실행 되기 때문에 다항법칙에 의해 f(n) = n² 이 됨

