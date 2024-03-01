## SQL 알아보기

- SQL이란?

  - DBMS에 존재하는 데이터를 관리하기 위한 프로그래밍 언어다.

  - DBMS에서 각각의 자료를 조회, 생성, 수정, 삭제할 수 있도록 한다.

- MYSQL => 세계적인 오픈 소스 관계형 데이터베이스 관리 시스템이다.

- 테이블 삭제

  ```
  DROP TABLE IF EXISTS `course`;
  ```

- 테이블 생성

  ```
  CREATE TABLE `course` (
      `course_name` VARCHAR(50) NOT NULL,
      `course_cost` INT NOT NULL,
      `course_date` DATETIME NOT NULL,
      PRIMARY KEY(`course_name`)
  );
  ```

- 레코드 삽입

  ```
  INSERT INTO course values ('Progamming', '3000', '2015-09-07');
  ```

- 데이터 조회

  ```
  SELECT {컬럼명} FROM {테이블명} {조건문};

  //ORDER BY를 활용한 정렬

  //내림차순
  SELECT * FROM cours ORDER BY course_cost DESC;

  //오름차순
  SELECT * FROM cours ORDER BY course_cost ASC;
  ```
