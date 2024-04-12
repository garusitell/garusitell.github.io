---
title: "[웹서버프로그래밍] 시험공부"
excerpt: "이해가 되지 않는 손코딩"

categories:
  - NCS
tags:
  - [NCS]

permalink: /NCS/Midterm exam/

toc: true
toc_sticky: true

date: 2024-04-12
last_modified_at: 2024-04-12
---

## 🦥 웹서버 프로그래밍

### 1주차

####  환경변수 설정

JDK 환경 변수 설정 -> 시스템 변수 새로만들기 ->  
 변수이름 : JAVA_HOME  
 변수값 :  C:\01developkt\jdk-17

 path -> 더블클릭 -> 새로만들기 ->  
 %JAVA_HOME%bin

#### 프로젝트 생성 JSP 예제
file -> New -> Dynamic Web Project  

Apache Tomcat v10.1  
Dynamic web module version 5.0 설정  

웹 모듈 설정화면에서 "Gemerate web.xml deployment descriptor 체크  

#### 배포 서술자(web.xml)  
 -  웹 어플리케이션의 환경설정 정보를 담은 파일  
 -  WAS(Web Application Server)가 처음 구동될 떄 이 파일을 읽어 설정 내용을 톰캣에 적용  
 - 서블릿 설정, 필터 설정 , 웰컴 파일 목록 등의 설정을 할 수 있음

 #### 프로젝트 생성 및 JSP예제.

 예제 helloJSP.jsp
 ``` javascript
 <%@ page language="java" contentType="text/html; charset=UTF-8"
pageEncoding="UTF-8"%>
<%!
String str1 = "JSP";
String str2 = "안녕하세요..!!";
%>
<body>
<h2>처음 만들어보는 <%= str1 %></h2>
<p>
<%
out.println(str2 + str1 + "입니다. 열공합시다^^*");
%>
</p>
</body>
 ```

 ### 2주차
 
 가장 간단한 메뉴 추가  
 `index.jsp`
 ``` html
<html>
    <%!
    String str1 = "백건효";
    String str2 = "안녕하세요!"
    %>

    <head>
        <meta chatset = "UTF-8">
        <title>Insert title here</title>
    </head>
    <body>
        <nav>
            <ul>
                <li><a href="input.jsp">명함입력</a></li> //#으로 들어간다 하이퍼링크
                <li><a href="serach.jsp">명함검색</a></li>
                <li><a href="#">홈으로</a></li>
            </ul>
        </nav>

        <h2>처음 만들어보는 <%= str1 %>/h2>
            <p>
                <% 
                out.println(str2 + str1 + "입니다.")
                %>
            </p>
    </body>
</html>

 ```
 `search.jsp`
 ```html
 <html>
    <body>
        <div>
            <table border = "1" width = "550" height ="300">
                <tr height = "20%">
                    <th width = "15%">이름</th>
                    <th width = "20%">폰번호</th>
                    <th width = "25%">이메일</th>
                    <th width = "40%">주소</th>
                </tr>
                <tr align = "center">
                    <td>이름</td>
                    <td>번호</td>
                    <td>이메일</td>
                    <td>주소</td>
                </tr>
                <tr align = "center">
                    <td>이름1</td>
                    <td>번호1</td>
                    <td>이메일1</td>
                    <td>주소1</td>
                </tr>
            </table>
        </div>
    </body>
</html>
 ```

 `input.jsp`
 ```html
 <body>
    <div align = "center"></div>
    <table border = "1" width = "550" height = "300">
        <tr align = "center">
            <td>이름</td>
            <td><input type = "text" name = "textName" size = "10"></td>
        </tr>
        <tr align = "center">
            <td>폰번호</td>
            <td><input type = "text" name = "txtPhone" size = "15"></td>
        </tr>
        <tr align = "center">
            <td>메일</td>
            <td><input = "text" name = "txtMail" size = "30"></td>
        </tr>
        <tr align = "center">
            <td>주소</td>
            <td><input type = "text" name = "txtAdress" size = "50"></td>
        </tr>
        <tr algin = "center">
            <tr>
                <td colspan = "2">
                    <button type = "submit">저장</button>
                    <button type = "reset">취소</button>
                </td>
            </tr>
        </tr>
    </table>
</body>
 ```

 ### 3주차

 #### 데이터베이스란?
- 우리가 매일 접하게 되는 거의 모든 웹 애플리케이션은 데이터베이스를 사용한다.
- JSP에서는 JDBC(JAVA DATABASE CONNECTIVIY)를 통해 데이터베이스와 연동

#### 설치
Express Edtion 21c -> c:/OracleXE 

#### table 만들기

`DDL(Data Defintaion Language)`
``` sql
CREATE TABLE my_table(
  id NUMBER(10),
  name VARCHAR2(20)
);
```

`DML`
```sql
INSERT INTO my_table(id,name) VALUES (1,"aaa");

SELECT * FROM my_table;

UPDATE my_table set name = 'bbb' WHERE id = 1;

DELETE FROM my_table WHERE id = 1;
```

### 4주차
`search.jsp` -- update

```javascript
<%@ page import = "org.apache.jasper.tagplugins.jstl.core.Import"%>
<%@ page language = "java" contentType = "text/html; charset = UTF-8" pageEncoding = "UTF-8"%>
<%@ page import = "java.sql."%>
<!DOCTYPE html>
<html>
    <html>
        <head>
            <meta charset = "UTF-8">
            <title>명함 검색</title>
        </head>
        <body>

            <h1>명함 검색</h1>
            <form action = "serach.jsp" method = "post">
                <input type ="text" name = "keyword" placeholder = "검색어 입력">
                <input type ="submit" value = "검색">
            </form>
        </body>
    </html>
```
