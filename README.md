---

<aside>
⚠️ 
해당 정리는 데이터베이스를 처음 접하는 사람들을 위한 생성 및 사용방법으로서
순서에 맞게 시작하면 됩니다.

주의) 이 정리는 MySQL을 다운로드 받았다는 전제 조건하에 작성되었습니다.

</aside>

## 1. database 생성 및 선택

1. CREATE DATABASE DATABASE NAME

  2.  SHOW DATABASES 를 통해 생성된 데이터베이스 확인 가능 

1. USE DATABASE NAME 생성된 데이터베이스를 선택하는 쿼리문 
2. SHOW TABLES 란 생성된 TABLE을 확인할 수 있다. 

---

## 2.  database의 table 만들기

mysql> create table topic(

-> number int(11) not null auto_increment,

-> title varchar(100) not null,

-> text text null,

-> date datetime not null,

-> username varchar(100) null,

-> primary key(number)


);

위 내용은 예시임으로 참고만 하길 바랍니다. 

1. auto_increment 란 일종의 카운터 개념으로 table에 insert시 1씩 증가하며 값을 넣어줍니다. 
2. not null 은 해당 컬럼이 null이 아니도록 꼭 들어가야하는 값이다. 
3. null 은 not null과는 반대로서 값이 굳이 안들어가도 되는 부분이다. 
4. primary key란 식별할수있는 컬럼으로 주로 상품으로 따지면, 상품코드, 숫자 등 해당부분에 사용한다.

해당 table 컬럼생성은 보기 편하기 위하여 개행하여 작성하였지만,

한줄로 써도 되며, 위와같이 보기 편하게 작성하여도 된다.

---

## 3.  기본적인 쿼리

<aside>
⚠️ 여기 적히는 모든 쿼리문은 예시이며 사용할 시 컬럼명 등등 전부 변경해야함으로 
주의하시기 바랍니다.

</aside>

insert 쿼리 예시 

insert into topic (title,text,date,username) values('제목','내용',now(),'pain developer');

select 쿼리 예시

select * from topic;

기본적으로 topic의 모든 컬럼을 불러오는 쿼리문

실무에서는 데이터가 너무 많아 보장할 수 없는 큰 오류가 발생할 수 있음으로 적절한 쿼리문을 설계 후 사용하기를 권고합니다. 

필자는 이런식으로 사용함 (주) select * topic limit = 5;  ( limit= 최대 불러올 개수 )

주로 select문을 많이 사용하니 여러가지 쿼리문을 알아두는게 좋습니다. 

order by now asc; 정도 

해당 쿼리문을 해석하자면 컬럼을 now를 기준으로 순서정렬 한 것이다. 

예시로는 게시판의 게시물을 정렬 후 처리 하는 용도에서 많이 사용합니다. 

그 외에 다른 데이터 확인에도 필수 불가결 함.

delete 쿼리 예시

delete * from topic;

말 그대로 삭제하는 쿼리문이며 위와같은 쿼리를 실행시킬 시 topic안에있는 모든 컬럼과 데이터를 삭제합니다. 

테스트를 하는것이라면 상관은 없지만 실무, 작업등 꼭 확인 후 실행하길 바랍니다.
## 4. union

비슷한 쿼리값을 하나의 쿼리로 묶을때 사용함.

```sql
select product_id,( 'store2' ) as store , store2 as price
from Products
where store2 is NOT NULL

union

select product_id,( 'store3' ) as store , store3 as price
from Products
where store3 is NOT NULL;
```

---

## 5. sum case

말 그대로 sum과 조건문인 case가 합쳐진 형태

```sql
select product_id, sum( 
case when store = 'buy'
then -price
else price
end 
from Products
order by product_id desc;

```

---
