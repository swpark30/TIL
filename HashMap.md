### HashMap 정리

> HashMap은 Map 인터페이스를 구현한 대표적인 Map컬렉션이다. Map 인터페이스를 상속하고 있기 때문에 Map의 성질을 그대로 가지고 있다.
>
> Map은 키와 값으로 구성된 Entry 객체를 저장하는 구조를 가지고 있는 자료구조이며, 여기서 키와 값은 모두 객체이다.
>
> 값은 중복저장 될 수 있으나 키는 중복저장 될 수 없고, 만약 기존에 저장된 키와 동일한 키로 값을 저장하면 기존의 키값은 없어지고 새로운 값으로 대치된다.

##### HashMap

- HashMap은 내부에 '키'와 '값'을 저장하는 자료 구조를 가지고 있다. HashMap은 해시 함수를 통해 '키'와 '값'이 저장되는 위치를 결정하므로, 사용자는 그 위치를 알 수 없고, 삽입되는 순서와 들어 있는 위치 또한 관계가 없다. 

  ![image-20220810005330681](HashMap.assets/image-20220810005330681.png)

##### HashMap 선언

- HashMap을 생성하려면 키 타입과 값 타입을 파라미터로 주고 기본생성자를 호출하면 된다. HashMap은 저장공간보다 값이 추가로 들어오면 List처럼 저장공간을 추가로 늘리는데 List처럼 저장공간을 한 칸씩 늘리지 않고 약 두배로 늘린다. 여기서 과부하가 많이 발생하기 때문에 초기에 저장할 데이터 개수를 알고 있다면 Map의 초기 용량을 지정해주는 것이 좋습니다. 

  ```java
  HashMap<String, String> map1 = new HashMap<String, String>();	// HashMap생성
  HashMap<String, String> map2 = new HashMap<>();	// 생성과정에서 파라미터 타입 생략 가능
  HashMap<String, String> map3 = new HashMap<>(map1);	// map1의 모든 값을 가진 HashMap 생성
  HashMap<String, String> map4 = new HashMap<>(10);	// 초기 용량 지정
  HashMap<String, String> map5 = new HashMap<String, String>(){{	// 초기값 지정
      put("a","b");
  }};
  ```

##### HashMap 값 추가

- HashMap에 값을 추가하려면 HashMap선언후 put(key, value)값을 입력해 주면 된다. 이때 설정한 HashMap의 타입과 같은 타입의 Key, Value값을 입력해 주어야 하며, 만약 입력되는 키 값이 HashMap내부에 존재하면 새로 입력되는 값이 이전값을 덮어 쓰게 된다.

  ```java
  HashMap<integer, String> map = new HashMap<>();	// 위 설명처럼 파라미터 타입 생략 가능
  
  // 값 추가
  map.put(1, "rok");
  map.put(2, "ho");
  map.put(3, "jeon");
  ```

##### HashMap 값 삭제

- HashMap 내부에 있는 값을 삭제하려면 remove(key) 메소드를 사용하면 된다. 키 값으로만 요소를 제거할 수 있으며 만약 모든 요소를 제거하고 싶으면

  clear() 메소드를 사용하면 된다.

  ```java
  HashMap<Integer, String> map = new HashMap<Integer, String>(){{	// 초기값 설정
     put(1, "rok");
     put(2, "ho");
     put(3, "jeon");
  }};
  
  map.remove(1);	// key값 1 제거(rok이 없어짐)
  map.clear();	// 내부에 있는 모든 key값 제거
  ```

##### HashMap 값 출력

- HashMap을 출력하는 방법에는 다양한 방법이 있다. 그냥 print하게 되면 {}로 묶어 Map의 전체 key값, value가 출력하고,  특정 key값의 value를 가져오고싶다면 get(key)를 사용하면 되고, 전체를 출력하려면 entrySet()이나 keySet()메소드를 활용하여 Map의 객체를 반환받은 후 출력하면 된다. entrySet()은 key와 value 모두가 필요할 경우 사용하며 keySet()은 key 값만 필요할 경우 사용하는데 key값만 받아서 get(key)를 활용하여 value도 출력할 수도 있기에 어떤 메소드를 선택하든지 간에 큰 상관이 없어 대부분 코드가 간단한 keySet을 활용하시던데 key값을 이용해서 value를 찾는 과정에서 시간이 많이 소모되므로 많은 양의 데이터를 가져와야 한다면 entrySet()이 좋다.

  ```java
  HashMap<Integer,String> map = new HashMap<Integer,String>(){{	//초기값 지정
      put(1,"rok");
      put(2,"ho");
      put(3,"jeon");
  }};
  		
  System.out.println(map); 	//전체 출력 : {1 = rok, 2 = ho, 3 = jeon}
  System.out.println(map.get(1));	//key값 1의 value얻기 : rok
  		
  //entrySet() 활용
  for (Entry<Integer, String> entry : map.entrySet()) {
      System.out.println("[Key]:" + entry.getKey() + " [Value]:" + entry.getValue());
  }
  //[Key]:1 [Value]:rok
  //[Key]:2 [Value]:ho
  //[Key]:3 [Value]:jeon
  
  //KeySet() 활용
  for(Integer i : map.keySet()){ //저장된 key값 확인
      System.out.println("[Key]:" + i + " [Value]:" + map.get(i));
  }
  //[Key]:1 [Value]:rok
  //[Key]:2 [Value]:ho
  //[Key]:3 [Value]:jeon
  ```

  