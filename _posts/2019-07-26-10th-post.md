---
categories: post
title: FTZ-9

---
<h1>FTZ 9번 문제</h1>

___

<br>
<strong>Hint</strong>
<br>


![1](https://user-images.githubusercontent.com/39820421/61951387-d3f90b00-afeb-11e9-95b2-2197311d6141.png)

<br> 해당 문제는 Buffer overflow 문제이다.<br>
___

![2](https://user-images.githubusercontent.com/39820421/61951388-d3f90b00-afeb-11e9-9a40-42eed3e9de47.png)

<br> hint에 나온 경로로 이동해 임의값을 넣어보았지만 아무 동작도 하지 않았다.<br>
<br> gdb로 해당 파일을 분석하고자 하였지만 권한이 없었기 떄문에 ~/tmp 경로에 파일을 만들어 분석하였다 <br>
___

![3](https://user-images.githubusercontent.com/39820421/61951389-d491a180-afeb-11e9-864b-ffec2ac94d0b.png)
<br>hint의 소스코드를 보면 buf의 크기는 10인데 fgets 함수에서는
40까지 입력 받을 수 있기 떄문에 취약점이 발생하고
if문을 보면 buf2가 "go" 라는 문자열이면 Good skill을 출력하고
쉘을 획득 할 수 있다고 되어있지만 buf2는 입력받지 않기 때문에
입력 가능한 buf 문자열에 overflow를 시켜 공격을 시도해야한다.<br>
___
![4](https://user-images.githubusercontent.com/39820421/61951390-d491a180-afeb-11e9-9370-fd41af09a1ab.png)

<br>gcc로 컴파일을 하여 gdb로 main 문을 열었다.<br>
fgets와 strncmp함수의 거리를 계산해보자.

___
![5](https://user-images.githubusercontent.com/39820421/61951391-d491a180-afeb-11e9-8e1a-99dcbb60d425.png)
16진수인 해당 주소값을 넣고 둘을 계산해보면 10진수 16‬이라는 계산 결과가 나온다.

___
![6](https://user-images.githubusercontent.com/39820421/61951393-d52a3800-afeb-11e9-864d-b1340178313f.png)
A를 16만큼 채우고 go라는 문자를 채우면 buf2에 값이 들어가 해당 문제가 풀리게 된다.

___
![7](https://user-images.githubusercontent.com/39820421/61951392-d52a3800-afeb-11e9-85f2-c4205bec90fc.png)
