---
title: "TYPESCRIPT_TodoList"
excerpt: "SETUP"

categories:
  - Categories8
tags:
  - [tag1, tag2]

permalink: /categories8/TYPESCRIPT_TodoList/

toc: true
toc_sticky: true

date: 2024-09-24
last_modified_at: 2024-09-24
---

### ☘️ TYPESCRIPT_TodoList만들기

### TodoList를 TypeScript를 사용하여 만들어 보았다.

1. db.json을 만들어준 후 package.json의 script에 아래 코드를 추가해준다.

```js
 "server": "json-server --watch db.json --port 4000",
```

2. yarn server로 실행

App.tsx에서 data를 불러올 수 있도록 axios를 사용하여 연결시켜준다.

```js
// test.js
import axios from "axios";

export type Todo = {
  id: string,
  title: string,
  completed: boolean,
};

export type Paginate<T> = {
  data: T[],
  first: number,
  items: number,
  last: number,
  next: number | null,
  pages: number,
  prev: number | null,
};

export async function getTodos(): Promise<Paginate<Todo>> {
  const res = await axios.get("http://localhost:4000/todos", {
    params: {
      _page: 1, // 페이지 번호
      _per_page: 25, // 페이지 당 항목 수
    },
  });

  const data: Paginate<Todo> = res.data;
  return data;
}

getTodos().then((data) => console.log(data));
```

App.tsx에서 데이터를 추가, 삭제, 수정하는 코드를 추가해준다.
props로 custom type을 내려주어 적용될 수 있도록 설정

```js
// App.tsx
import { useEffect, useState } from "react";
import "./App.css";
import { getTodos, type Todo } from "./test";
import axios from "axios";

type ToggleTodo = Omit<Todo, "title">;

const App = () => {
  const [todoList, setTodoList] = useState<Todo[]>([]);

  // 서버 데이터 초기 렌더링
  useEffect(() => {
    getTodos().then((data) => setTodoList(data.data));
  }, []);

  const [title, setTitle] = useState("");

  const handleTitleChange = (e: React.ChangeEvent<HTMLInputElement>) => {
    setTitle(e.target.value);
  };

  const handleAddTodo = async () => {
    if (title.trim() === "") {
      return;
    }

    const newTodo: Todo = {
      id: crypto.randomUUID(), // 고유한 id 생성
      title,
      completed: false,
    };

    try {
      // 새로운 todo를 서버에 추가
      const response = await axios.post("http://localhost:4000/todos", newTodo);

      // 성공적으로 추가된 후 상태 업데이트
      setTodoList((prev) => [...prev, response.data]);

      // 입력 필드 초기화
      setTitle("");
    } catch (error) {
      console.error("Error adding todo:", error);
    }
  };

  const handleDelete = async (id: Todo["id"]) => {
    try {
      // 서버에서 할 일을 삭제
      await axios.delete(`http://localhost:4000/todos/${id}`);

      // 삭제 후 상태에서 해당 할 일을 제거
      setTodoList((prev) => prev.filter((todo) => todo.id !== id));
    } catch (error) {
      console.error("error", error);
    }
  };

  // 할 일의 완료 상태를 토글하는 함수
  const handleToggleTodo = async ({ id, completed }: Omit<Todo, "title">) => {
    try {
      // 서버에 PATCH 요청을 통해 완료 상태 변경
      await axios.patch(`http://localhost:4000/todos/${id}`, {
        completed: !completed,
      });

      // 상태에서 해당 할 일의 완료 상태를 업데이트
      setTodoList((prev) =>
        prev.map((todo) =>
          todo.id === id ? { ...todo, completed: !completed } : todo
        )
      );
    } catch (error) {
      console.error("Error", error);
    }
  };

  return (
    <>
      <TodoList
        todoList={todoList}
        onDeleteClick={handleDelete}
        onToggleClick={handleToggleTodo} // prop 이름을 일치시킴
      />
      <input type="text" value={title} onChange={handleTitleChange} />
      <button onClick={handleAddTodo}>등록</button>
    </>
  );
};

type TodoListProps = {
  todoList: Todo[];
  onDeleteClick: (id: Todo["id"]) => void;
  onToggleClick: (toggleTodo: ToggleTodo) => void; // prop 이름을 수정
};

const TodoList = ({
  todoList,
  onDeleteClick,
  onToggleClick,
}: TodoListProps) => {
  return (
    <>
      {todoList.map((todo) => (
        <TodoItem
          key={todo.id}
          {...todo}
          onDeleteClick={onDeleteClick}
          onToggleClick={onToggleClick}
        />
      ))}
    </>
  );
};

type TodoItemProps = Todo & {
  onDeleteClick: (id: Todo["id"]) => void;
  onToggleClick: (toggleTodo: ToggleTodo) => void;
};

const TodoItem = ({
  id,
  title,
  completed,
  onDeleteClick,
  onToggleClick,
}: TodoItemProps) => {
  return (
    <div>
      <div>id: {id}</div>
      <div>title: {title}</div>
      <div>completed: {`${completed}`}</div>
      <button onClick={() => onDeleteClick(id)}>삭제</button>
      <button onClick={() => onToggleClick({ id, completed })}>
        완료 토글
      </button>
      <hr />
    </div>
  );
};

export default App;

```
