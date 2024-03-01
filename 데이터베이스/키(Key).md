## 키(Key)

- 테이블

  - 하나의 데이터베이스는 여러 개의 테이블을 가진다.

  - 테이블은 같은 속성(열)을 가진 튜플(행)의 모음이다.

<br />

- 테이블 생성

  ```
  CREATE TABLE `테이블 이름`
  (
      {컬럼명 1} {자료형 1},
      {컬럼명 2} {자료형 2},
      {컬럼명 3} {자료형 3},
      ...
  );
  ```

<br />

- 테이블 제약 조건 - 기본

  - NOT NULL : NULL 값 비허용, 중복 허용

  - UNIQUE : NULL 값 허용, 중복 비허용

  - PRIMARY KEY : NULL 비허용, 중복 비허용, 테이블당 하나씩

  - DEFAULT : 해당 컬럼의 기본값을 설정

- 테이블 제약 조건 - 외래키

  - 특정한 학생이 다른 강의를 등록하는 상황이면, 등록 테이블은 "학생번호"와 "강의번호"를 **참조**해야한다. => 이러한 기능을 위해 **외래키**(각각 테이블에 있는 기본키인 학생 번호, 강의 번호)가 제공된다.

  - 만약 학생 테이블에 없는 학생을 추가하려는 경우 오류가 발생한다.

  - **외래키는 하나의 테이블이 다른 테이블을 참조할 때 사용한다.**

  - 학생 <- 등록 -> 강의

  ```
  CREATE TABEL registraion
  (
      student_id INT,
      lecture_id INT,
      date DATETIME,
      FOREIGN KEY (student_id) PEFERENCES student(student_id),
      FOREIGN KEY (lecture_id) PEFERENCES lecture(lecture_id)
  );
  ```
