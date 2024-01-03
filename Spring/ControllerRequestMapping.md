
### Controller
- URL에 따른 요청을 처리하는 메서드를 담아두는 클래스임을 나타낸다

### @RequestMapping
- 어떤 URL 요청에 대하여 실행되는 메서드임을 나타낸다

```java
@Controller
public class DemoController {
    @RequestMapping("home")
    public String index() {
        return "home.html";
    }
```