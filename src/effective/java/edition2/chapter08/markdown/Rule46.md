### 규칙 46 for 문보다는 for-each 문을 사용하라
***

* 릴리즈 1.5 이전 버전과 이후 버전에서 Collection 을 순회할 때의 차이점 _(test_step_01 예제)_
* for-each 문에서 ':' 기호는 '안에 있는' 이라고 읽는다.
* for-each 문의 장점은 여러 컬렉션에 중첩되는 순환문을 만들어야 할 때 더 빛난다.
* _(test_step_02 예제)_ 의 버그를 찾아보자.
  * 바깥쪽 순환문에서 사용하는 컬렉션 반복자의 next() 메서드가 너무 많이 호출된다는 것이다.
  * 원래 대로라면 바깥쪽 순환문 안에서 카드 종류별로 한 번만 호출되어야 했는데(4회),
  * 안쪽 순환문에서 호출되다보니 카드 숫자별로 한 번씩 호출 호출되는 것이다.(13회)
  * 그래서 suit 컬렉션이 너무 빨리 소진되어서 결국 **NoSuchElementException 이 발생**하고 만 것이다.
  * 해결책으로 _(test_step_02_1, test_step_02_2 예제) 를 통해서 확인하자.
* _(test_step_03 예제)_ 의 버그를 찾아보자.
  * 원래는 36개의 조합을 출력해야 했지만, 6개의 조합만을 출력 함

* for-each 문은 전통적인 for 문에 비해 명료하고 버그 발생 가능성도 적으며, 성능도 for 문에 뒤지지 않는다.
* 그러나 불행히도 아래 3가지 경우에 한해서 for-each 문을 적용할 수 없음을 주의하자.
  * **필터링**: 컬렉션을 순회하다가 특정 원소를 삭제할 필요가 있다면, 반복자를 명시적으로 사용해야 한다. (반복자의 remove 함수)
  * **변환**: 리스트나 배열을 순회하다가 그 원소 가운데 일부 또는 전부를 변경해야 한다면, 원소의 값을 수정하기 위해서 리스트 반복자나 배열 첨자가 필요하다.
  * **병렬 순회**: 여러 컬렉션을 병렬적으로 순회해야 하는 상황에서 변수를 명시적으로 제어할 필요가 있을 때 필요하다.