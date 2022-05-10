
1. <수정(edit)>, <저장(save)> 아이콘 찾기
-----------------------------------------

 구현에 필요한 아이콘을 구글링하여 찾기

   --> "TodoList.vue"에서 휴지통 아이콘 태그 확인
          <i class="far fa-trash-alt" aria-hidden="true"></i>
   --> "fa-trash-alt"을 키워드로 구글링
   --> 첫번째 링크를 클릭
   --> 검색된 아이콘 생성태그가 다음과 같이 실습코드와 약간 다름
          <i class="fas fa-trash-alt"></i>   // "fas"가 아닌 "far"
   --> 현재 페이지 안의 검색창에 "trash" 입력검색
   --> 결과 화면의 오른쪽 두번째줄 두번째 위치에 유사 아이콘 발견
   --> 클릭
   --> 결과 화면이 다음 태그를 가지고 있고 찾고자 하는 태그와 일치
          <i class="far fa-trash-alt"></i>
   --> 비슷한 요령으로 "trash" 대신에 "edit", "save" 검색
   --> 다음과 같은 태그 발견
          <i class="far fa-edit"></i>
          <i class="far fa-save"></i>
   --> "TodoList.vue"에서 발견된 2개 아이콘 사용



2. 소스코드 분석
----------------

  "TodoList.vue" (in <vue-todo>)
  ------------------------------

   --> 실행결과 화면(복수개의 todo아이템이 그려짐)을 만드는
        해당 html 태그가 다음 후보 발견(why: "v-for"가 반복문인가?)
          <li v-for="(todoItem, index) in propsdata" ... >
   --> 구글링("vue.js v-for") 결과 vue.js 프레임워크의 반복지시
        디렉티브인 것을 확인


  "TodoItem.vue" (in <vue-todo-with-editing>)
  -------------------------------------------

   --> <template> 내용 분석결과 todoitem 디스플레이 화면과 수정화면이        동일 공간을 공유하여 교차적으로 출력되도록 다음 2개라인이 
       사용된다고 추정.  

          <div class="content" v-show="!isEditing">
          .........
          <div class="content" v-show="isEditing">

   --> 구글링확인("v-show"가 true/false이면 해당태그가 보임/안보임).
        내부변수(isEditing) 값에 따라 "v-show"값이 결정됨.


  "App.vue" (in <vue-todo>)
  -------------------------

   --> "todoItems" 클래스 멤버변수가 전체 "todoList"를 배열로 저장함.

   --> 자식 클래스인 "TodoList"에 다음 지시자로 배열이 전달됨(구글링)
           ... v-bind:propsdata="todoItems" ...

   --> "TodoList"는 위의 <propsdata>를 받아 다음과 같이 저장/활용
           props: ['propsdata'],

   --> 또다른 자식 클래스인 "TodoInput"가 새로운 todo 아이템을 보내면
        이를 받아 "todoItems"에 추가(this.todoItems.push(todoItem);)

   --> 또다른 자식 클래스인 "TodoFooter"에서 <Clear All> 버튼 클릭시
        이벤트 전달로 "todoItems" 전체삭제(this.todoItems = [];)

   --> "todoItems" 클래스 멤버변수는 하드디스크에 실시간 업데이트 됨

   --> 구글링으로 하드디스크 액세스(localStorage) 메소드/변수 확인

         clear(), getItem(), key(), removeItem(), setItem(), length

   --> 이를 사용하여 todo 아이템 내용 수정 기능 구현


