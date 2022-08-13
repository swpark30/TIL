### Org JSON 파싱

> JSON이란?
> 
> Object, Array, Key-Value 형태로 이루어져 있으며 String, Int, Long, Boolean 등의 타입을 지원

##### Object

- Object는 {  }로 감싸여 있는 것을 말한다. 
  
  ```json
  {
    "title": "how to get stroage size",
    "url": "https://codechacha.com/ko/get-free-and-total-size-of-volumes-in-android/",
    "draft": false,
    "star": 10
  }
  ```

- 위의 JSON 코드에는 1개의 Object가 있고 그 안에 title, url, draft, star라는 4개의 key와 그에 해당하는 value를 가지고 있다.

##### Key-Value

- key-value는 위의 예제를 들면 "title"이 key, "how to get storage size"가 value에 해당 한다. key는 꼭 `"..."` 처럼 콜론으로 감싸져야 한다. value는 String 타입인 경우 `"..."`으로 표현하고 Boolean이나 Integer는 그냥 쓰면 된다.
  
  ```json
  "title": "how to get stroage size",
  ```

##### Array

- Array는 `[ ]` (square bracket)으로 감싸여 있는 것을 말한다.
```json
{
  "posts": [
      {
          "title": "how to get stroage size",
          "url": "https://codechacha.com/ko/get-free-and-total-size-of-volumes-in-android/",
          "draft": false
      },
      {
            "title": "Android Q, Scoped Storage",
            "url": "https://codechacha.com/ko/android-q-scoped-storage/",
            "draft": false
      },
      {
            "title": "How to parse JSON in android",
            "url": "https://codechacha.com/ko/how-to-parse-json-in-android/",
            "draft": true
      }
  ]
}
```

##### JSON 파싱
1. 간단한 Key-Value만 있는 JSON
```java
import org.json.JSONArray;
import org.json.JSONObject;

public void jsonParsing1() {
    String jsonString = "{\"title\": \"how to get stroage size\","
            + "\"url\": \"https://codechacha.com/ko/get-free-and-total-size-of-volumes-in-android/\","
            + "\"draft\": false,"
            + "\"star\": 10"
            + "}";

    // JSONObjet를 가져와서 key-value를 읽습니다.
    JSONObject jObject = new JSONObject(jsonString);
    String title = jObject.getString("title");
    String url = jObject.getString("url");
    Boolean draft = jObject.getBoolean("draft");
    int star = jObject.getInt("star");

    System.out.println("title: " + title);
    System.out.println("url: " + url);
    System.out.println("draft: " + draft);
    System.out.println("star: " + star);
}
```

결과
```log
title: how to get stroage size
url: https://codechacha.com/ko/get-free-and-total-size-of-volumes-in-android/
draft: false
star: 10
```

2. 하위에 여러 Object가 있는 JSON
```java
import org.json.JSONArray;
import org.json.JSONObject;

public void jsonParsing2() {
    String jsonString =
        "{"
        +   "\"post1\": {"
        +       "\"title\": \"how to get stroage size\","
        +       "\"url\": \"https://codechacha.com/ko/get-free-and-total-size-of-volumes-in-android/\","
        +       "\"draft\": false"
        +"  },"
        +   "\"post2\": {"
        +       "\"title\": \"Android Q, Scoped Storage\","
        +       "\"url\": \"https://codechacha.com/ko/android-q-scoped-storage/\","
        +       "\"draft\": false"
        +   "}"
        +"}";

    // 가장 큰 JSONObject를 가져옵니다.
    JSONObject jObject = new JSONObject(jsonString);

    // 첫번째 JSONObject를 가져와서 key-value를 읽습니다.
    JSONObject post1Object = jObject.getJSONObject("post1");
    System.out.println(post1Object.toString());
    System.out.println();
    String title = post1Object.getString("title");
    String url = post1Object.getString("url");
    boolean draft = post1Object.getBoolean("draft");
    System.out.println("title(post1): " + title);
    System.out.println("url(post1): " + url);
    System.out.println("draft(post1): " + draft);
    System.out.println();

    // 두번째 JSONObject를 가져와서 key-value를 읽습니다.
    JSONObject post2Object = jObject.getJSONObject("post2");
    System.out.println(post2Object.toString());
    System.out.println();
    title = post2Object.getString("title");
    url = post2Object.getString("url");
    draft = post2Object.getBoolean("draft");
    System.out.println("title(post1): " + title);
    System.out.println("url(post1): " + url);
    System.out.println("draft(post1): " + draft);
}
```

결과
```log
{"draft":false,"title":"how to get stroage size","url":"https://codechacha.com/ko/get-free-and-total-size-of-volumes-in-android/"}

title(post1): how to get stroage size
url(post1): https://codechacha.com/ko/get-free-and-total-size-of-volumes-in-android/
draft(post1): false

{"draft":false,"title":"Android Q, Scoped Storage","url":"https://codechacha.com/ko/android-q-scoped-storage/"}

title(post1): Android Q, Scoped Storage
url(post1): https://codechacha.com/ko/android-q-scoped-storage/
draft(post1): false
```

3.  Array가 있는 JSON
```java
import org.json.JSONArray;
import org.json.JSONObject;

public void jsonParsing3() {
    String jsonString =
    "{"
    +   "\"posts\": ["
    +       "{"
    +           "\"title\": \"how to get stroage size\","
    +           "\"url\": \"https://codechacha.com/ko/get-free-and-total-size-of-volumes-in-android/\","
    +           "\"draft\": false"
    +       "},"
    +       "{"
    +           "\"title\": \"Android Q, Scoped Storage\","
    +           "\"url\": \"https://codechacha.com/ko/android-q-scoped-storage/\","
    +           "\"draft\": false"
    +       "},"
    +       "{"
    +           "\"title\": \"How to parse JSON in android\","
    +           "\"url\": \"https://codechacha.com/ko/how-to-parse-json-in-android/\","
    +           "\"draft\": true"
    +       "}"
    +   "]"
    +"}";

    // 가장 큰 JSONObject를 가져옵니다.
    JSONObject jObject = new JSONObject(jsonString);
    // 배열을 가져옵니다.
    JSONArray jArray = jObject.getJSONArray("posts");

    // 배열의 모든 아이템을 출력합니다.
    for (int i = 0; i < jArray.length(); i++) {
        JSONObject obj = jArray.getJSONObject(i);
        String title = obj.getString("title");
        String url = obj.getString("url");
        boolean draft = obj.getBoolean("draft");
        System.out.println("title(" + i + "): " + title);
        System.out.println("url(" + i + "): " + url);
        System.out.println("draft(" + i + "): " + draft);
        System.out.println();
    }
}
```

결과
```log
title(0): how to get stroage size
url(0): https://codechacha.com/ko/get-free-and-total-size-of-volumes-in-android/
draft(0): false

title(1): Android Q, Scoped Storage
url(1): https://codechacha.com/ko/android-q-scoped-storage/
draft(1): false

title(2): How to parse JSON in android
url(2): https://codechacha.com/ko/how-to-parse-json-in-android/
draft(2): true
```