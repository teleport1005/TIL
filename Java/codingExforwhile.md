## Java Practice Challenges 

1. 한 정수를 입력받는다. 이 정수는 잔고이다.
이후 반복해서 인출할 돈을 정수로 계속 입력받는다.
인출한 결과를 "성공: 잔고"의 형태로 출력하고,
잔고가 부족할 경우 "잔고가 부족합니다". 라고 출력 뒤 프로그램을 종료하여라.

```Java
        Scanner scanner = new Scanner(System.in);
        System.out.println("잔고를 입력하세요.");
        int money = scanner.nextInt();
        System.out.println("인출할 금액을 입력하세요.");
        while (true){
            int spend = scanner.nextInt();
            if (spend > money){
                System.out.println("잔고가 부족하여 인출할 수 없습니다.");
                break;
            }
            int save = money - spend;
            money -= spend;
            System.out.println(spend + "원이 인출되었습니다. 잔액은 " + save + "입니다.");
        }
```
```
잔고를 입력하세요.
1000
인출할 금액을 입력하세요.
300
300원이 인출되었습니다. 잔액은 700입니다.
```
---
2. 세 명의 사람들에 대한 정보가 개행문자로 구분된 이름(문자열)이 세 번, 개행문자로 구분된 체온(정수)이 세 번 입력된다.  
이 중 체온이 38도가 넘는 사람들의 이름을 출력해 보자.

```Java
        Scanner scanner = new Scanner(System.in);
        String[] names = new String[3];
        int[] tempereture = new int[3];

        System.out.println("3명의 이름을 입력하세요.");
        for (int i = 0; i < 3; i++) {
            names[i] = scanner.nextLine();
        }
        System.out.println("체온을 차례대로 입력하세요.");
        for (int i = 0; i < 3; i++) {
            tempereture[i] = scanner.nextInt();
        }
        System.out.println("체온이 38도가 넘는 사람들은 아래 분들입니다.");

        for (int i = 0; i < 3; i++) {
            if (tempereture[i] > 38) {
                System.out.println(names[i]);
            }
```
```
3명의 이름을 입력하세요.
김건강
김비실
김독감
체온을 차례대로 입력하세요.
36
35
39
체온이 38도가 넘는 사람들은 아래 분들입니다.
김독감
```
---
3. 한 정수를 입력받는다. 이후 이 정수를 거듭제곱하며 1의 자리를 확인하면서, 몇 번 거듭제곱 했을 때 다시 원래의 숫자의 1의 자리랑 일치하는지 출력하여라.  
 한번만 거듭제곱해도 본래 숫자가 되면 결과는 1이다
 ```Java
         Scanner scanner = new Scanner(System.in);
        System.out.println("정수를 입력해 주세요.");
        int n = scanner.nextInt();
        int result = n;
        int count = 1;
        while (result % 10 != n % 10 || result != n) {
            result *= n; // 입력된 숫자를 거듭제곱하여 결과값 갱신
            result %= 10; // 결과값의 1의 자리 수만 남기기 위해 10으로 나눈 나머지 값 저장
            count++; // 반복 횟수 증가
        }

        System.out.println("입력된 숫자를 거듭제곱하여 원래 숫자의 1의 자리와 일치하는 최소 횟수: " + count);
 ``` 
 ```
 정수를 입력해 주세요.
38
입력된 숫자를 거듭제곱하여 원래 숫자의 1의 자리와 일치하는 최소 횟수: 1
 ```
 > 답이 계속 1로만 출력된다  
 > result에 n * n을 할당하면 n의 2승부터 계산이 가능하다
---
4. 1월 1일의 요일과 2월 29일의 유무가 정수, 불린으로 주어진다.  

이때 1월 1일의 요일은,
```
0 - 월요일, 1 - 화요일, 2 - 수요일, 3 - 목요일, 4 - 금요일, 5 - 토요일, 6 - 일요일
```
로 입력된다. 각 달의 1일이 무슨 요일인지 1월부터 12월까지 순서대로 출력하는 코드를 작성하시오.
```Java
        Scanner scanner = new Scanner(System.in);
        System.out.println("이번 년도의 1월 1일은 무슨 요일인가요?");
        System.out.println("다음의 형식에 맞추어 입력해 주세요.");
        System.out.println("0 - 월요일, 1 - 화요일, 2 - 수요일, 3 - 목요일, 4 - 금요일, 5 - 토요일, 6 - 일요일");
        int dayOfWeek = scanner.nextInt();
        System.out.println("이번 년도에 2월 29일이 있다면 true, 없다면 false를 입력해 주세요");
        boolean february29 = scanner.nextBoolean();

        int[] dayInMonth = {31, (february29 ? 29 : 28), 31, 30, 31, 30, 31, 30, 31, 30, 31, 30};
        String[] weekdays = {"월", "화", "수", "목", "금","토", "일"};

        System.out.println("이번 년도 각 달의 1일은");

        for (int i = 0; i < dayInMonth.length; i++) {
            System.out.println((i + 1) + "월 1일은 " + weekdays[dayOfWeek % 7] + "요일");
            dayOfWeek = (dayOfWeek + dayInMonth[i]) % 7;
```
```
이번 년도의 1월 1일은 무슨 요일인가요?
다음의 형식에 맞추어 입력해 주세요.
0 - 월요일, 1 - 화요일, 2 - 수요일, 3 - 목요일, 4 - 금요일, 5 - 토요일, 6 - 일요일
0
이번 년도에 2월 29일이 있다면 true, 없다면 false를 입력해 주세요
true
이번 년도 각 달의 1일은
1월 1일은 월요일
2월 1일은 목요일
3월 1일은 금요일
4월 1일은 월요일
5월 1일은 수요일
6월 1일은 토요일
7월 1일은 월요일
8월 1일은 목요일
9월 1일은 토요일
10월 1일은 화요일
11월 1일은 목요일
12월 1일은 일요일
```
 