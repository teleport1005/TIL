## Java Practice Challenges 

1. 사용자로부터 정수를 입력받아, 그 수가 양수인지, 음수인지, 아니면 0인지를 판별하여 출력하는 프로그램을 작성해 보세요.
```Java
   Scanner scanner = new Scanner(System.in);
        System.out.println("정수를 입력해 보세요.");
        int num = scanner.nextInt();
         if (num > 0){
             System.out.println(num + " 는 양수입니다.");
         } else if (num < 0){
             System.out.println(num + " 는 음수입니다.");
         } else {
             System.out.println(num + " 는 0입니다.");
         }
```
---
2. 축구리그에서는 승점을, 승리시 3점 무승부시 1점, 패배시 0점을 획득한다.   
남은 경기와 현재 승점과 목표 승점이 주어졌을 때, 남은 경기에서 목표 승점을 넘을 수 있으면 필요한 최소 승수를, 없으면 최고 승점을 출력하여라.
```java
        Scanner scanner = new Scanner(System.in);
        System.out.println("남은 경기 수를 입력하세요");
        int leftGame = scanner.nextInt();
        System.out.println("현재 승점을 입력하세요.");
        int nowWin = scanner.nextInt();
        System.out.println("목표 승점을 입력하세요.");
        int winner = scanner.nextInt();

        int wishwin = (winner - nowWin);
         if (wishwin <= leftGame * 3){
             int mustWin = wishwin / 3;
             System.out.println("앞으로 최소 " + mustWin + " 번 이겨야 합니다.");
         } else {
             int weLose = nowWin + leftGame * 3;
             System.out.println("목표 승점은 도달이 불가합니다. 최고 승점은 " + weLose + "입니다." );
```
---
3. 1인치는 2.54 센티미터이다. 1inch = 2.54cm
사용자에게 정수를 두개 입력받는다.
첫번째 정수가 0이라면 두번째 정수는 센티미터이고,
첫번째 정수가 1이라면 두번째 정수는 인치이다.
센티미터는 해당 길이의 인치로, 인치는 해당 길이의 센티미터로 소수점 2째 자리까지 출력하여라.
```Java
        Scanner scanner = new Scanner(System.in);
        System.out.println("cm를 inch로 변환하고 싶으시면 0, inch를 cm로 변환하고 싶으시면 1을 입력해 주세요.");
        int cmInchComputer = scanner.nextInt();
        System.out.println("계산하고 싶은 길이를 입력하세요.");
        int howLong = scanner.nextInt();
        if (cmInchComputer == 0){
            double whatInch = howLong / 2.54;
            System.out.printf("%dcm는 %.2finch입니다.\n", howLong, whatInch);
        } else {
            double whatCm = howLong * 2.54;
            System.out.printf("%dinch는 %.2fcm입니다.\n", howLong, whatCm);
```
> printf의 사용법과 소숫점 자리 출력 방법에 대해 익숙해지자.

