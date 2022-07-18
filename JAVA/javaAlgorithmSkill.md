# 220718 공부
<img src="https://cdn.pixabay.com/photo/2020/03/10/16/47/moon-4919501__340.jpg"></img>
```
날카로운 달의 날이 서서히 차오른다.
꽉 찬 둥근 공의 형상으로 오늘의 달이 떠오른다.
동에서 떠올라 하늘을 가로지른다.
그저 돌았을 뿐인데 목적지에 도달한다.
강렬한 관성의 힘은 달을 그리로 이끈다.
별의 빛을 받아 반짝이는 달은 지구의 중력을 받아 돌며 어느덧 그 안으로 쏙 빠져들었다.
```
\
\
</br>

```java
public class aa1 {
    public static void main(String[] args) {
        int a = 5;
        s(a); // number=5
        s2(a); // 66number
    }
    public static void s(int intVal){
        System.out.println("number" + "=" + intVal);
    }
    public static void s2(int intVal){
        System.out.println(intVal + '=' + "number");
    }
}

//해결법

Integer.toString(num1)
과 같이 감싸준다.
```
\
\
</br>
### 실전적인 스트림 활용을 위한 예시
```java
public class dfhgdfsh {
    public static void main(String[] args) {
//        Stream<Integer> numbers2 = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
//        Optional<Integer> sum2 = numbers2.reduce(Integer::sum);
//        sum2.ifPresent(s -> System.out.println("sum2: " + s)); // sum2 : 55

        Stream<Integer> numbers2 = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

//        double sum2 = numbers2.mapToInt(Integer::intValue).average().orElse(0);
        double sum2 = numbers2.mapToInt(qq->qq).average().orElse(0);
        //위 두개는 동일한 결과과

       System.out.println(sum2);

        int[] L1 = new int[]{1,2,3,4,5,6,7,8,9,10};
        System.out.println(Arrays.toString(L1)); //  [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
//        Stream<Integer> a1 = Arrays.stream(L1); 오류
        IntStream a1 = Arrays.stream(L1);
        double AVG1 = a1.average().orElse(0);
        System.out.println(AVG1); // 5.5


        ArrayList<Integer> L2 = new ArrayList<>(Stream.of(1,2,3,4,5,6,7,8,9,10).collect(Collectors.toList()));
        System.out.println(L2.toString()); // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
//        IntStream a2 = L2.stream(); 이거는 오류
        Stream<Integer> a2 = L2.stream();
        double AVG2 = a2.filter(q->q%3==0).mapToInt(e->3*e).average().orElse(0);
        System.out.println(AVG2); //18.0
    }
}

```
\
\
</br>

#### 단순한 출력 with 스트림
```
public class ws001 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int[] arr = new int[]{10, 11,12,13,14,15,16,17,18,19};
        System.out.println("-----원소 10개 출력-----");
        Arrays.stream(arr).forEach(x -> System.out.print(x + " "));
        System.out.println();
        System.out.println("-----원소 10개 중 짝수만 출력-----");
        Arrays.stream(arr).filter(x->x%2==0).forEach(x -> System.out.print(x + " "));
        System.out.println();
        System.out.print("-----바꿀 위치 입력 : ");
        int n = sc.nextInt();
        System.out.print("-----수 입력 : ");
        int num = sc.nextInt();
        arr[n] = num;
        System.out.println("-----원소 10개 출력-----");
        Arrays.stream(arr).forEach(x -> System.out.print(x + " "));

    }
}
```
\
\
</br>
```java
import java.util.Arrays;
import java.util.stream.IntStream;

public class self001 {
    public static void main(String[] args) {
        getAverageOfIntparams(1,2,3,4,5,6,7);
        //[1, 2, 3, 4, 5, 6, 7]
        //4.0
        int[] nowIntlist = new int[]{11,22,33};
        getAverageOfIntparams(nowIntlist);
        //[11, 22, 33]
        //22.0
    }

    public static void getAverageOfIntparams (int... params){
        System.out.println(Arrays.toString(params));
        IntStream q = Arrays.stream(params);
        double AVG = q.average().orElse(111);
        System.out.println(AVG);
    }
}

```

```


```