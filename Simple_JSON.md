### Simple JSON

> json-simple 라이브러리는 JSON파싱을 지원함
>
> .java파일에서 JSONObject jsonObj = new JSONObject(); 를 입력후 import를 시켜주면 라이브러리가 생성된다.
>
> 만약 없다면 pom.xml에서 dependency를 추가해준다.

##### MAVEN 환경이 아닐경우

- 환경이 MAVEN이 아닌경우에는 jar파일을 add해주어야 한다.

- 다음과 같이 의존성을 추가해준다.

  ```java
  <dependency>
      <groupId>com.googlecode.json-simple</groupId>
      <artifactId>json-simple</artifactId>
      <version>1.1.1</version>
  </dependency>

##### JSON 파일 읽기

- .json 파일에서 Reader를 통해 텍스트를 읽어드리는 방법

  ```java
  import java.io.FileReader;
  import org.json.simple.JSONObject;
  import org.json.simple.JSONArray;
  import org.json.simple.parser.JSONParser;
  
  public class jsonFileRead{
      public static void main(String[] args) throws IOException {
          // .json 파일 READ
          Reader reader = new FileReader("File Path");
          
          // reader를 Object로 parse
          JSONParser parser = new JSONParser();
          Object obj = parser.parse(reader); 
          
          // 아래 code로 이어짐
      }
  }
  ```

- 위의 코드절차를 통해서 file을 object로 만들어야 한다.

##### JSON객체 단건(JSONObject)

- {"name" : "rokrok", "job" : "Programmer", "age" : "31"}

- 파일에서 읽은 값이 위와 같이 단건의 json객체라면 바로 JSONObject에 담으면 된다.

  ```java
  // 상단 코드에 이어 
  
  // obj를 JsonObject로 cast
  JSONObject jsonObj = (JSONObject)obj;
  
  System.out.println((String)jsonObj.get("name"));  // rokrok출력
  ```

- JSONObject에서 get한 뒤에는 (String)으로 캐스팅하는 것이 좋다.

##### JSON객체 다건(JSONArray)

- [{"name" : "rokrok", "job" : "Programmer", "age" : "31"}, {"name" : "kwak", "job" : "Datascientist", "age" : "29"}]

- 파일에서 읽은 값이 위와 같이 다건의 json객체라면 JSONArray에 담았다가 JSONObject로 담아야 한다.

  ```java
  // 상단 코드에 이어 
  
  // obj를 JsonArray로 cast
  JSONArray jsonArr = (JSONArray)obj;
  
  // jsonArr에서 하나씩 JSONObject로 cast해서 사용
  if (jsonArr.size() > 0){
      for(int i=0; i<jsonArr.size(); i++){
          JSONObject jsonObj = (JSONObject)jsonArray.get(i);
          
          System.out.println((String)jsonObj.get("name")); 
      }
      // rokrok, kwak 출력
  }
  ```

##### 다건 JSON객체가 JSON내부에 있는 경우

- {

  "day" : "20220806",

  "user" : [{"name" : "rokrok", "job" : "Programmer", "age" : "31"}, {"name" : "kwak", "job" : "Datascientist", "age" : "29"}]

  }

- 파일에서 읽은 값이 json안에 있는 array라면 jsonObject와 jsonArray를 반복해서 사용하면 된다.

  ```java
  // 상단 코드에 이어 
  
  // obj를 우선 JSONObject에 담음
  JSONObject jsonMain = (JSONObject)obj;
  
  // jsonObject에서 jsonArray를 get함
  JSONArray jsonArr = (JSONArray)jsonMain.get("user");
  
  // jsonArr에서 하나씩 JSONObject로 cast해서 사용
  if (jsonArr.size() > 0){
      for(int i=0; i<jsonArr.size(); i++){
          JSONObject jsonObj = (JSONObject)jsonArray.get(i);
          
          System.out.println((String)jsonObj.get("name")); 
      }
      // rokrok, kwak 출력
  }
  ```

- 만약 json 다건중에 또 json다건이 포함된 파일인 경우, jsonArray로 담아 반복문으로 또 jsonArray를 꺼내면 된다.

