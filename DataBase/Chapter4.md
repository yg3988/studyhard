# SQL

## 질의어와 SQL

SQL : Structured Qurey Language의 약자, 1974년 IBM의 System R project에서 개발된 Sequel이란 언어에 기초한다. 표준 질의어로 채택되어 널리 쓰이는 관계형 질의어로 관계 대수나 관계 해석은 확실한 이론적 배경을 제공하나 상용으로 쓰이기에는 어렵고 적절치 않음
- SQL은 자연어와 유사하고 비절차적 언어이므로 사용하기 용이함

## SQL의 구성 : DDL & DML

SQL은 크게 DDL과 DML로 구성됨  
DDL : 데이터 정의 언어(Data Definition Language)
  - 데이터 저장 구조를 명시하는 언어
  - 테이블 스키마의 정의, 수정, 삭제  
DML : 데이터 조작 언어(Data Manipulation legal Language)
  - 사용자가 데이터를 접근하고 조작할 수 있게 하는 언어
  - 레코드의 검색, 삽입, 삭제, 수정

## 데이터 정의 언어

테이블 생성(create table)  
기본키, 외래키 설정  
테이블 삭제(drop table)  
테이블 수정(alter table)

종류
  - 테이블 생성
  - 테이블 삭제
  - 테이블 수정

필드의 Data type 종류

![DataType](../.src/DBtype.jpg)
## 테이블 생성

형식
> create table <테이블이름> (<필드리스트>)
  - <필드리스트>는 '필드명 데이터타입'

![create1](../.src/createTable1.jpg)

키워드 not null은 해당 필드에 널을 허용하지 않는다는 것을 의미한다.

## 기본키, 외래키 설정
테이블을 생성할 기본키 역할을 하는 필드를 지정
![create2](../.src/createTable2.jpg)
pk_department : 제약식의 이름
  - 제약식 : 테이블에 부적절한 자료가 입력되는 것을 방지하기 위해서 여러 가지 규칙을 적용해 놓은 것
not null이 정의 되어있지 않아도 제약식에 의해 not null로 정의됨

![create3](../.src/createTable3.jpg)
외래키까지 포함된 테이블 생성의 예

> foreign key(dept_id) references department(dept_id)

다른 테이블의 기본키를 참조한다는 뜻이다.

## 테이블 삭제

형식
>drop table <테이블 이름>

내부 정의 뿐만 아니라 instance도 삭제한다.

다른 테이블에서 외래키로 참조되는 경우에는 삭제할 수 없다.

## 테이블 수정

기존의 테이블에 새로운 필드를 추가하거나 기존의 필드를 삭제

형식

>alter table <테이블이름> add <추가할 필드>
>alter table <테이블이름> drop column <제거할 필드>

필드를 삭제할 경우 수정할 수 없다.

## 기본키, 외래키 관련 주의사항

R<sub>1</sub>이 R<sub>2</sub> 테이블을 외래키로 참조한다면 삭제할 수 없다.  
R<sub>2</sub> 테이블을 삭제하려면 R<sub>1</sub>을 먼저 삭제하던지, 외래키를 해체해야 한다.

## 데이터 조작 언어

레코드 삽입  
레코드 수정  
레코드 삭제  
레코드 검색

## 레코드 삽입

형식
>insert into <테이블 이름> (<필드리스트> values (<값리스트>))

<필드리스트> : 삽입에 사용될 테이블의 필드들 - 생략 가능함
<값리스트> : <필드리스트>의 순선에 맞춰 삽입될 값 - 생략 가능함

<필드리스트>에 나열되지 않은 필드에 대해서는 널값이 입력됨  
<필드리스트>를 생략할 경우 <값리스트>에는 테이블을 생성할 때 나열한 필드의 순서에 맞춰서 값을 나열

>insert into department (dept_id, dept_name, office) values ('920', '컴퓨터공학과', '201호')

<필드리스트> : 생략된 컬럼에는 null값이 저장됨
필드리스트와 값리스트는 1:1 사상된다.

삽입 명령문에 필드 이름을 나열할 경우 그 순서는 테이블을 생성할 때 지정한 순서와 반드시 일치할 필요는 없다.

not null로 설정된 필드는 널 값이 들어갈 수 없는 필드이기 때문에 insert문의 <필드리스트>에서 생략할 수 없다.

>insert into department values ('923', '산업공학과', '207호')

<필드리스트>를 사용하지 않고 데이터를 삽입하는 예

## 레코드 수정

형식 - instance 수정
>update <테이블 이름>
>set <수정내역>
>where <조건>

<수정내역> : 대상 테이블의 필드에 들어가는 값을 수정하기위한 산술식, ','를 이용하여 여러 필드에 대한 수정 내역을 지정

<조건>
  - 대상이 되는 레코드에 대한 조건을 기술
  - 관계대수에서 선택 연산의 조건식과 같은 의미
  - 테이블의 모든 레코드에 대해 수정을 적용하려면 where 절을 생략

예
>update student
>set    year = year + 1

student 테이블에서 모든 학생들의 학년을 하나씩 증가

>update professor
>set    position='교수', dept_id='923'
>where  name='고희석'

professor 테이블에서 '고희석' 교수의 직위를 '교수'로 수정하고 학과번호를 '923'으로 수정

## 레코드 삭제

형식 - 테이블 삭제 : drop(유의)
>delete from  <테이블 이름>
>where        <조건>

where절에 지정된 조건을 만족하는 레코드를 삭제
where절이 생략되면 테이블에서 모든 레코드를 삭제

>delete from  professor
>where        name = '김태석'

professor 테이블에서 이름이 '김태석'인 교수를 삭제한다.
delete문을 이용하여 테이블의 모든 레코드를 삭제하더라도 테이블은 삭제되지 않는다.

## 레코드 삽입 시 주의사항

외래키로 사용되는 필드에 대해 데이터를 삽입할 때
- 참조하는 테이블의 해당 필드에 그 값을 먼저 삽입해야 한다.
외래키로 사용되는 필드의 값을 수정할 때
- 외래키가 참조하는 테이블에 삽입되어 있는 값으로만 수정 가능
외래키로 참조되는 필드를 가지고 있는 테이블에서 레코드를 삭제할 경우에도 오류가 발생할 수 있음

## 레코드 검색

Select : SQL에서 가장 많이 사용하고, 중요하며, 복잡하다.

종류
- 기본구조
- 재명명 연산
- like 연산
- 집합 연산
- 외부 조인
- 집계 함수
- 널의 처리
- 중첩 질의

### 기본 구조
형식
>select <필드리스트>
>from   <테이블리스트>
>where  <조건>

select - 필수 : 질의 결과로 출력할 필드들의 리스트, 관계대수의 추출연산에 해당한다.  
from - 필수 : 질의 실행 과정에 필요한 테이블들의 리스트를 나타내며, 관계대수의 카티션 프로덕트에 해당한다.
where : 검색되어야 하는 레코드에 대한 조건, 관계대수의 선택연산에서 사용되는 조건식과 동일하다. 생략가능

>select name, dept_name
>from   department, student
>where  department.dept_id = student.dept_id

의미
- from절에 나열된 department테이블과 student 테이블을 카티션 프로덕트
- where절에 지정된 조건식을 만족하는 레코드만 선택
  - 같은 이름의 필드가 두 개 이상의 테이블에 나타날 때 혼동을 피하기 위해 '테이블이름.필드이름'으로 표현
- 최종적으로 name 필드와 dept_name 필드의 값 만을 추출하라.

>select address
>from   student

student 테이블에서 모든 학생들의 주소를 추출

>select distinct  address
>from             student

student 테이블에서 모든 학생들의 주소를 추출
중복된 레코드를 제거하고 검색하는 명령어 : distinct

>select *
>from   student

from 절에 나타난 테이블에서 모든 필드의 값을 추출할 경우에는 select 절에 모든 필드를 명시할 필요 없이 '\*'를 사용

>select name, 2012-year_emp
>from   professor

select절에 필드이름 외에 산술식이나 상수의 사용이 가능하다.

## 레코드의 순서 지정(Order by)
검색 결과를 정렬하여 출력하는 기능  
select문 맨 마지막에 다음과 같은 order by절을 추가  
형식
>order by <필드리스트>

오름차순을 기본으로 하며 <필드리스트>에 여러 개의 필드를 나열할 경우 나열된 순서대로 정렬

>select   name, stu_id
>from     student
>where    year = 3 or year = 4
>order by name, stu_id

order by절 이하 name으로 오름차순으로 정렬하고 같은 이름에 대해서는 stu_id의 오름차순으로 정렬

내림차순은 해당 필드 이름 뒤에 desc 라는 키워드를 삽입해야 한다. 오름차순은 default이다.

>select   name, stu_id
>from     student
>where    year = 3 or year = 4
>order by name desc, stu_id

## 재명명 연산

테이블이나 필드에 대한 재명명
- 실제 테이블 이름이 수정되거나 필드 이름이 바뀌는 것이 아님
- 질의를 처리하는 동안만 일시적으로 사용
- 표현이 단순화하거나, 동일 이름이 존재할 경우에 사용

>student  student.name, department.dept_name
>from     student, department
>where    student.dept_id = department.dept_id

>student  s.name, d.dept_name
>from     student s, department d
>where    s.dept_id = d.dept_id

동일 테이블이 두 번 사용 가능

>student  s2.name
>from     student s1, student s2
>where    s1.address = s2.address and s1.name = '김광식'

## 필드의 재명명

질의 실행 결과를 출력할 때 원래 필드의 이름 대신 재명명된 이름으로 출력하고자 할 때 사용

>select name, position, 2012-year_emp
>from   professor

>select name 이름, position 직위, 2012-year_emp 재직연수
>from   professor

## Like 연산

문자열에 대해서 일부분만 일치하는 경우를 찾아야 할 때 사용
'=' 연산자 대신에 'like'를 이용함- '='는 정확히 일치하는 경우에만 사용

형식
>where  <필드이름>
>like   <문자열패턴>

<필드이름>에 지정된 <문자열패턴>이 들어 있는지를 판단

문자열 패턴 종류
- '\_' : 임의의 한 개 문자를 의미한다.
- '%' : 임의의 여러 개 문자를 의미한다.

>select *
>from   student
>where  name like '김%'

student 테이블에서 김씨 성을 가진 학생들을 찾는 질의

>select *
>from   student
>where  resident_id like '%-2%'

student 테이블에서 여학생들만을 검색

## 집합연산

관계대수의 집합 연산인 합집합(union), 교집합(intersect), 차집합(minus)에 해당하는 연산자

형식
><select문1> <집합연산자> <select문2>

조건  
<select문1>과 <select문2>의 필드의 개수와 데이터타입이 서로 같아야 함.

### union

>select name from student
>union
>select name from professor

student 테이블의 학생 이름과 professor 테이블의 교수 이름을 합쳐서 출력

union 연산자는 연산 결과에 중복되는 값이 들어갈 경우 한번만 출력한다. 만약 중복을 제거하고 싶지 않다면 union all 연산자를 사용한다.

### intersect

>select   s.stu_id
>from     student s, department d, takes t
>where    s.dept_id = d.dept_id and
>         t.stu_id = s.stu_id and
>         dept_name='컴퓨터공학과' and
>         grade = 'A+'

>select   stu_id
>from     student s, department d
>where    s.dept_id = d.dept_id and
>         dept_name='컴퓨터공학과'
>intersect
>select   stu_id
>from     takes
>where    grade = 'A+';

컴퓨터공학과 학생들 중에서 교과목에 상관없이 학점을 'A+' 받은 학생들의 학번을 검색

### MINUS

>select stu_id
>from   student s, department d
>where  s.dept_id = d.dept_id and
>       dept_name = '산업공학과'
>minus
>select stu_id
>from   takes
>where  grade = 'A+'

산업공학과 학생들 중에서 한 번이라도 'A+'를 받지 못한 학생들의 학번을 검색

## 외부 조인

>select   title, credit, year, semester
>from     course, class
>where    course.course_id = class.course_id

모든 교과목들에 대해 교과목명, 학점수, 개설 년도, 개설 학기를 검색  
강좌로 개설된 적이 있는 교과목에 대해서만 검색된다. '이산수학', '객체지향언어'교과목들은 class 테이블에 저장되어 있지 않기 때문에 검색결과에 포함하지 못한다.

### 왼쪽 외부조인

연산자의 왼쪽에 위치한 테이블의 각 레코드에 대해서 오른쪽 테이블에 조인 조건에 부합하는 레코드가 없을 경우에도 검색 결과에 포함  
생성되는 결과 레코드에서 오른쪽 테이블의 나머지 필드에는 널 삽입

>select           title, credit, year, semester
>from             course
>left outer join  class
>using (course_id)

>select title, credit, year, semester
>from   course, class
>where  course.course_id = class.course_id(+)

### 오른쪽 외부조인
>select           title, credit, year, semester
>from             course
>right outer join class
>using            (course_id)

>select title, credit, year, semester
>from   course, class
>where  course.course_id(+) = class.course_id

### 완전 외부조인

양쪽 테이블에서 서로 일치하는 레코드가 없을 경우, 해당 레코드들도 결과 테이블에 포함시키며 나머지 필드에 대해서는 모드 널을 삽입

>select           title, credit, year, semester
>from             course
>full outer join  class
>using            (course_id)

## 집계 함수

통계 연산 기능 제공

종류
- count : 데이터의 개수를 구한다.
- sum : 데이터의 합을 구한다.
- avg : 데이터의 평균 값을 구한다.
- max : 데이터의 최대 값을 구한다.
- min : 데이터의 최소 값을 구한다.

select 절과 having절에서만 사용가능 (select 필드리스트 뒤에)
sum, avg는 숫자형 데이터 타입을 갖는 필드에만 사용가능

## count

형식
>count (distinct <필드이름>)

해당 필드에 값이 몇 개인지 출력  
null은 계산에서 제외됨  
단, <필드이름>에는 필드 이름 대신 '\*'가 사용된 경우에는 레코드의 개수를 계산

>select count(\*)
>from   student
>where  year = 3

student 테이블에서 3학년인 학생의 수

>select count(dept_id)
>from   student

student 테이블에서 dept_id 필드에 값이 몇 개인지를 출력

>select count(distinct dept_id)
>from   student

student 테이블에서 dept_id에 중복되는 데이터를 제외한 개수를 출력

>select count(\*)
>from   student s, department d
>where  s.dept_id = d.dept_id and
>       d.dept_name = '컴퓨터공학과'

컴퓨터 공학과 학생 수를 출력

## sum

형식

>sum(<필드이름>)

>select sum(2012-year_emp)
>from   professor

전체 교수들의 재직연수 합

>select sum(sal)
>from   emp
>where  job = 'ANALYST'

업무가 'ANALYST'인 직원들의 급여의 합을 출력

>select sum(sal)
>from   emp e, dept d
>where  e.dept_no = d.dept_no and dname = 'RESEARCH'

부서이름이 'RESEARCH'인 직원들의 급여의 합을 출력

## avg

형식
>avg(<필드이름>)

>select avg(2012 - year_emp)
>from   professor

전체 교수의 평균 재직 연수를 출력

## min, max

형식
>max(<필드이름>)
>min(<필드이름>)

>select max(sal)
>from   emp e, dept d
>where  e.dept_no = d.dept_no and dname = 'ACCOUNTING'

부서이름이 'ACCOUNTING'인 직원들 중에서 최대 급여가 얼마인지 출력

## group by

select 절에 집계 함수가 사용될 경우 다른 필드 select 절에 사용할수가 없음  
group by를 이용하면 그룹별로 집계함수 적용 가능

형식
>group by <필드리스트>

- group by 절은 select문에서 where절 다음에 위치
- group by에 지정된 필드의 값이 같은 레코드들끼리 그룹을 지어 각 그룹별로 집계 함수를 적용한 결과를 출력

>select     dept_id, count(\*)
>from       student
>group by   dept_id

student 테이블에서 학과번호별로 레코드의 개수를 출력

>select     dept_name, count(\*)
>from       student s, department d
>where      s.dept_id = d.dept_id
>group by   dept_name

학과번호 대신 department 테이블과 조인하여 학과 이름이 출력되록 수정

>select   dname, count(\*), avg(sal), max(sal), min(sal)
>from     emp e, dept d
>where    e.dept_no = d.dept_no
>group    dname

emp, dept 테이블에서 부서별 직원수, 평균급여, 최대급여, 최소급여를 출력

## having

그룹에 대한 조건을 명시할 때 사용
  - group에 대한 조건은 where절에 사용불가
  - having절을 이용해야 함

형식
>having <집계함수 조건>

>select   dept_name, count(\*), avt(2012-year_emp), max(2012-year_emp)
>from     professor p, department d
>where    p.dept_id = d.dept_id
>group by dept_name
>having   avg(2012-year_emp) >= 10

평균 재직연수가 10년 이상인 학과 중에서 과의 이름과 교수 숫자, 평균 재직연수, 최대 재직연수를 출력

where절과 having절, group by절을 모두 함께 사용할 경우
 -  where절에 명시된 조건을 만족하는 레코드들을 검색
 -  group by절에 명시도니 필드의 값이 서로 일치하는 레코드들 끼리 그룹을 지어 집계함수를 적용
 -  마지막으로 그 집계 함수를 적용한 결과들 중에서 having절을 만족하는 결과만 골라서 출력

## NULL의 처리

널을 검색하는 방법

형식
><필드이름> is null
><필드이름> in not null

>select stu_id
>from   takes
>where  grade is null

takes 테이블에서 아직 학점이 부여되지 않은 학생의 학번을 검색

>select stu_id
>from   takes
>where  grade <> 'A+'

takes 테이블에서 학점이 'A+'가 아닌 학생들의 학번을 검색

grade 필드의 ㄱ밧이 널인 레코드에 대해서는 질의 결과에 포함되지 않음

## View

기존 테이블들로부터 생성되는 가상의 테이블  
테이블처럼 물리적으로 생성되는 것이 아니라 기존의 테이블들을 조합  
기능
- 특정 사용자에게 테이블의 내용 중 일부를 숨길 수 있기 때문에 보안의 효과
- 복잡한 질의의 결과를 뷰로 만들어서 사용하게 되면 질의를 간단히 표현할 수 있음

### 뷰 생성

생성된 뷰는 테이블과 동등하게 사용

형식
> create or replace view  <뷰이름> as
>                         <select문>

or replace 키워드를 추가하면 <뷰이름>과 같은 뷰가 이미 존재하는 경우 기존의 뷰를 지우고 새로 생성

<select문> : 뷰 생성에 사용될 select문

대부분의 DBMS에서는 사용자 계정에는 뷰 생성 권한이 부여되지 않음  
관리자 계정이 아닌 사용자 계정으로 로그인하여 뷰를 생성하려면 뷰 생성과 관련된 권한이 부여되어야함.

>create or replace view v_takes as
>                               select  stu_id, class_id
>                               from    takes

grade 필드를 제외한 나머지 필드만으로 구성된 뷰를 생성

>select *
>from   v_takes
>where  stu_id = '1292502'

v_takes 뷰에 대해 select문을 실행

뷰에 대해서 insert, update, delete문을 실행  
뷰를 생성할때 마지막 행에 with read only 키워드를 추가하면 읽기 전용 뷰가 생성되어 insert, update, delete문 사용 불가
