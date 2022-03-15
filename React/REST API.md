# 💡 API

---

API는 **어플리케이션 프로그래밍 인터페이스**(Application Programming Interface)를 나타내는 약어이다. 운영 체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스로 프로그램의 상호작용을 도와주는 매개체 역할을 한다.

# 💡 REST API ( RESTful Web services )

---

CRUD(Create, Read, Update, Delete) 연산을 수행하기 위해 **URI로 요청을 보내는 것**으로 메소드 형식을 사용해 요청을 보낸다. 이러한 REST 기반의 API를 웹으로 구현한 것이 REST API이다.

어떤 식으로 정보를 주고 받고 업데이트하고 삭제할 것인지 정해놓은 웹의 장점을 최대한 활용할 수 있는 아키텍처 스타일이다.

# 💡 REST API의 구성요소

---

- **Resource**

서버는 고유한 ID를 가지는 URI을 가지고 있으며, 클라이언트는 이러한 URI에 요청을 보냅니다.

- **Method**

서버에 요청을 보내기 위한 방식으로 GET, POST, PUT, DELETE등이 있습니다. CRUD 연산 중에서 처리를 위한 연산에 맞는 Method를 사용하여 서버에 요청을 보낸다.

- **Representation of Resource**

클라이언트와 서버가 데이터를 주고받는 형태로 json, xml, text, rss 등이 있다. 최근에는 Key, Value를 활용하는 json을 주로 사용한다.

# 💡 자주 쓰이는 메소드

---

- **GET**

서버에서 정보를 가져올 때 이미 존재하는 데이터의 정보를 가져올 때 사용하며 읽기용으로 활용한다.

- **POST**

새로운 데이터를 만들 때 사용한다.

- **PUT**

이미 존재하는 데이터의 정보를 업데이트할 때 사용한다.

- **DELETE**

이미 존재하는 데이터를 삭제할 때 사용한다.
