# 220717 공부
<img src="../assets/2207/0717start.jpg"></img>
```
해가 지고, 하루를 마친다. 필멸의 땅 위에 서있는 자들에게 남겨진 조언은
길을 잃었다.
속세의 염원을 담은 사람들의 목소리가 옅어져만 간다.
더 이상 꿈을 이야기하는 어리석은 자는 존재하지 않는다.
잿빛이 되어버린 도시에서, 살아남겠다는 우매한 말을 내뱉다간 바보 취급을
받게 될지도 모른다.
어찌됐든 내일도 해가 뜰 것이고, 아마 나는 이 도시를 뜰 것 같다.
남겨진 이들에게 전해야 할 말들을 적은 종이를 하늘에 던진다.
```
\
[JVM에 대하여](https://willseungh0.tistory.com/93?category=874438)

```
// Item중에서 가격이 1000 이상인 이름을 5개 선택하기
List<String> items = item.stream()
    			.filter(d->d.getPrices()>=1000)
                          .map(d->d.getName())
                          .limit(5)
                          .collect(tpList());

```
```
Stream<Integer> numbers = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
Optional<Integer> sum = numbers.reduce((x, y) -> x + y);
sum.ifPresent(s -> System.out.println("sum: " + s)); // 55

```
```
// Item중에서 가격이 1000 이상인 이름을 5개 선택하기
List<String> items = item.stream()
    			.filter(d->d.getPrices()>=1000)
                          .map(d->d.getName())
                          .limit(5)
                          .collect(tpList());

```

```
List<String> myList = Arrays.asList("a1", "a2", "b1", "c2", "c1");

myList
    .stream()							// 생성하기
    .filter(s -> s.startsWith("c"))			// 가공하기
    .map(String::toUpperCase)			// 가공하기
    .sorted()							// 가공하기
    .count(); // return 되는 값은 2

```

```java
        int sum = IntStream.of(1, 3, 5, 7, 9)
                .peek(System.out::println)
                .sum();
        peek은 stream연산에 영향을 주지 않고 그냥 중간에 한 번 출력을 해봄
```
```java
        Stream<String> a = Stream.of(1.0, 2.0, 3.0)
                .mapToInt(Double::intValue)
                .mapToObj(i -> "a" + i);
        a.forEach(System.out::println);
//        a1 
//        a2
//        a3
```

\
any 와 all의 활용
```java
IntStream stream1 = IntStream.of(30, 90, 70, 10);

IntStream stream2 = IntStream.of(30, 90, 70, 10);

 

System.out.println(stream1.anyMatch(n -> n > 80)); // true

System.out.println(stream2.allMatch(n -> n > 80)); // false
```
\
\
스트림으로 합과 평균 구하기
```java
IntStream stream1 = IntStream.of(30, 90, 70, 10);

DoubleStream stream2 = DoubleStream.of(30.3, 90.9, 70.7, 10.1);

 

System.out.println(stream1.sum()); // 200

System.out.println(stream2.average().getAsDouble()); // 50.5

```
\
\
collectors

> 스트림 요소의 수집 용도별 사용할 수 있는 Collectors 메소드는 다음과 같습니다.\
>>1. 스트림을 배열이나 컬렉션으로 변환 : toArray(), toCollection(), toList(), toSet(), toMap()
>>2. 요소의 통계와 연산 메소드와 같은 동작을 수행 : counting(), maxBy(), minBy(), summingInt(), averagingInt() 등
>>3. 요소의 소모와 같은 동작을 수행 : reducing(), joining()
>>4. 요소의 그룹화와 분할 : groupingBy(), partitioningBy()

```java
Stream<String> stream = Stream.of("HTML", "CSS", "JAVA", "PHP");

 

Map<Boolean, List<String>> patition = stream.collect(Collectors.partitioningBy(s -> (s.length() % 2) == 0));

 

List<String> oddLengthList = patition.get(false);

System.out.println(oddLengthList); // [CSS, PHP]

 

List<String> evenLengthList = patition.get(true);

System.out.println(evenLengthList); // [HTML, JAVA]
```
```java
import java.util.Optional;
public class ppp {
    public static void main(String []args){
        Optional<String> opt = Optional.ofNullable("자바 Optional 객체");
        System.out.println(opt.isPresent() ? opt.get() : null); // "자바 Optional 객체"
    }
}
```


```
스트림 구조는 크게 3가지로 나눈다.

1.     스트림생성

2.     중개 연산

3.     최종 연산

객체 집합.스트림생성().중개연산().최종연산()
```
>중개 연산\
>: Filter/ Map/ Peek/ Sorted/ Limit/ Distinct/ Skip/ mapToInt,maptToLong,mapToDouble etc.\
>
> -Filter\
List<String> names = Arrays.asList("jeong", "pro", "jdk", "java");\
Stream<String> a = names.stream().filter(x -> x.contains("o"));\
> \
-Map\
List<String> names = Arrays.asList("jeong", "pro", "jdk", "java");\
names.stream().map((x) ->{return x.concat("s");}).forEach(x -> System.out.println(x));\
> \
> -Limit\
스트림의 개수를 .limit(3)으로 지정하면 3개로 제한한다. (물론 중개연산이라 스트림 반환)\
List<Integer> ages = Arrays.asList(1,2,3,4,5,6,7,8,9);\
ages.stream().filter(x -> x>3).limit(3);\
-Distinct\
스트림의 요소가 예를 들어 1,2,1,2,1,2,1,2 일 때 .dinstinct()를 적용하면 1,2로 중복을 제거한다.\
> \
-Skip\
.skip(3) 이라고하면 처음3개의 요소는 제외하고 나머지 요소들로 새로운 stream을 생성한다.\
> \
-mapToInt, mapToLong, mapToDouble\
mapXXX 함수들은 해당 타입의 스트림으로 바꿔준다. 예를들어 “1”, “2”, “3”을 가진 스트림이 있었으면 maptoInt를 적용하면 1,2,3을 가진 스트림으로 변환해준다.

    #최종 연산

    : count(), min(), max(), sum(), average()/ reduce/ forEach/ collect/ iterator/ noneMatch, anyMatch, allMatch etc.
    -count(), min(), max(), sum(), average()



    -reduce
    
    Reduce는 누적된 값을 계산하는 함수다.
    
    여기서 b,c로 지정한 파라미터를 가지고 리턴한 결과(b+c)가 다시 b가 된고 다음 스트림의 요소가 c가 되어 계속 누적된다. 따라서 1+2+3인 6이 결과로 찍힌다.
    
    
    
    List<Integer> ages = new ArrayList<Integer>();
    ages.add(1); ages.add(2); ages.add(3); //1,2,3
    System.out.println(ages.stream().reduce((b,c) -> b+c).get()); //1+2+3=6


    -forEach
    
    forEach는 map이나 peek의 최종연산 버전이다. 각 요소를 돌면서 처리할 수 있도록 되어있다.
    
    
    List<Integer> ages = new ArrayList<Integer>();
    ages.add(1); ages.add(2); ages.add(3); //1,2,3
    Set<Integer> set = ages.stream().collect(Collectors.toSet());
    set.forEach(x -> System.out.println(x)); //1,2,3
    
    
    -collect
    
    Collect는 스트림의 값들을 모아주는 기능을 한다. toMap, toSet, toList로 해당 스트림을 다시 컬렉션으로 바꿔준다.
    
    
    
    -iterator
    
    Iterator는 Iterator<T>를 반환한다.
    
    
    
    List<String> names = Arrays.asList("jeong", "pro", "jdk", "java");
    Iterator<String> iter = names.stream().iterator();
    while(iter.hasNext()){
    System.out.println(iter.next()); //jeong, pro, jdk, java
    }
    
    
    -noneMatch, anyMatch, allMatch
    
    noneMatch는 최종적으로 얻은 스트림의 “모든” 요소들이 조건을 만족하지 “않는” 지를 판단해서 Boolean 값을 리턴한다.
    
    anyMatch는 스트림의 요소들 중 하나라도 조건을 만족하는 지 판단해서 boolean값을 리턴한다.
    
    allMatch는 스트림의 “모든” 요소들이 조건을 만족하는지를 판단해서 boolean값을 리턴한다.
    
    
    List<Integer> ages = new ArrayList<Integer>();
    ages.add(1); ages.add(2); ages.add(3); //1,2,3
    System.out.println(ages.stream().filter(x -> x>1).noneMatch(x ->x>2)); //false

```java
public class ppp {
    public static void main(String []args){
        List<String> names = Arrays.asList("jeong", "pro", "jdk", "java");
//        names.stream().map((x) -> x.concat("s")).forEach(x -> System.out.println(x));
        Stream<String> a = names.stream().filter(x -> x.contains("o")).map(x -> x.concat("s"));
        Set<String> s = a.collect(Collectors.toSet());
        System.out.println(s);
    }
}
```

```java
//일단 L은 Apple로 구성된 ArrayList입니다.
public static ArrayList<Apple> filterAppleByColor(ArrayList<Apple> inventory, Color color) {
        ArrayList<Apple> result = new ArrayList<>();
        for(Apple apple : inventory){
        if( apple.getColor().equals(color)){
        result.add(apple);
        }
        }
        return result;
        }
        //요런 함수 만들어서
        wantColorAppleList = filterAppleByColor(L, Blue);
//이런식으로 원하는 색의 사과만 꺼낼 수 있음.


//여기는 groupingBy의 활용 예시( 색으로 사과를 구분해본다. )
        Stream<Apple> a = L.stream().filter( x -> x.getWeight() > 5);
        Map<Color, List<Apple>> cc = a.collect(Collectors.groupingBy(Apple::getColor));
        System.out.println(cc.get(Red));


        //특정 조건으로 partitioning하는거
        Stream<Apple> a = L.stream().filter( x -> x.getWeight() > 105);
        Map<Boolean, List<Apple>> cc = a.collect(Collectors.partitioningBy(p->p.getWeight() > 200));
        System.out.println(cc);
```

```java

    // 스트림의 요리 개수 세기
    int count = menu.stream().map(d->1).reduce(0,(a,b)-> a+b)
```


[Stream에 관해 공부하고 정리해보자!!](https://mangkyu.tistory.com/112)
```java

List<String> names = Arrays.asList("Eric", "Elena", "Java");

boolean anyMatch = names.stream()
    .anyMatch(name -> name.contains("a"));
boolean allMatch = names.stream()
    .allMatch(name -> name.length() > 3);
boolean noneMatch = names.stream()
    .noneMatch(name -> name.endsWith("s"));


//개별 출력
names.stream().forEach(System.out::println);


```





\
\
\
마무리
```
내 모든 게 결국에는 가라앉아서
빛이 보이지 않는 곳에 내가 있다면
넌 노래를 불러줘
```
