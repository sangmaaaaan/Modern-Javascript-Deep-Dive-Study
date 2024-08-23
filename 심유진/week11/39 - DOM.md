# 39 - DOM

### DOM 🤔

HTML 문서의 계층적 구조와 정보를 표현하며 이를 제어할 수 있는 **API 프로퍼티와 메서드**를 제공하는 **트리자료구조**다 

- **노드 타입에 따라 필요한 기능**을 프로퍼티와 메서드의 집합인 DOM API로 제공 

![image.png](39%20-%20DOM%20e6886781091144a5b3847d49efff2b1d/image.png)

### HTML 내용 구조 , 스타일 변경하려면 ?

### 1. 요소 노드 취득

### 1.1 `id`로 취득

- **방법**: `document.getElementById(id)`
- **예시**:
    
    ```jsx
    javascript코드 복사
    const element = document.getElementById('myId');
    ```
    

### 1.2 태그 이름으로 취득

- **방법**: `document.getElementsByTagName(tagName)`
- **예시**:
    
    ```jsx
    javascript코드 복사
    const elements = document.getElementsByTagName('div'); // HTMLCollection 반환
    ```
    

### 1.3 `class`로 취득

- **방법**: `document.getElementsByClassName(className)`
- **예시**:
    
    ```jsx
    javascript코드 복사
    const elements = document.getElementsByClassName('myClass'); // HTMLCollection 반환
    ```
    

### 1.4 `querySelector`로 취득

- **방법**: `document.querySelector(selector)` 또는 `document.querySelectorAll(selector)`
- **예시**:
    
    ```jsx
    javascript코드 복사
    const element = document.querySelector('.myClass'); // 첫 번째 일치 요소 반환
    const elements = document.querySelectorAll('.myClass'); // NodeList 반환
    ```
    

### 2. **HTMLCollection과 NodeList**

- **HTMLCollection**: `getElementsByTagName` 또는 `getElementsByClassName` 메서드가 반환하는 라이브 컬렉션이다. DOM이 변경되면 컬렉션도 실시간으로 업데이트된다.
- **NodeList**: `querySelectorAll` 메서드가 반환하는 정적 리스트다. 특정 경우에만 live 객체로 동작하며 DOM이 변경되더라도 컬렉션은 변경되지 않는다.

### 3. **textContent**

- **개요**: 요소의 텍스트 내용을 설정하거나 취득한다. 텍스트에 포함된 HTML 태그는 무시됨.
- **사용법**:
    
    ```jsx
    const element = document.getElementById('myId');
    element.textContent = '새 텍스트 내용';
    ```
    

### 4. **innerHTML**

- **개요**: 요소의 HTML 콘텐츠를 설정하거나 취득합니다. HTML 태그를 포함한 문자열을 설정할 수 있다.
- **사용법**:
    
    ```jsx
    
    const element = document.getElementById('myId');
    element.innerHTML = '<p>새로운 <strong>HTML</strong> 내용</p>';
    ```
    

### 5. **노드 생성과 추가 (`Document.prototype.createElement(tagName)`)**

- **개요**: 새로운 요소를 생성하고 DOM에 추가합니다.
- **사용법**:
    
    ```jsx
    const newElement = document.createElement('div');
    newElement.textContent = '새로운 요소';
    document.body.appendChild(newElement); // DOM에 요소 추가
    ```
    

### 6. 노드 삽입

- **방법**: `Node.prototype.appendChild` 또는 `Node.prototype.insertBefore`
- **예시**:
    
    ```jsx
    
    const newElement = document.createElement('div');
    newElement.textContent = '삽입할 요소';
    
    const parentElement = document.getElementById('parentId');
    const referenceElement = document.getElementById('referenceId');
    
    parentElement.insertBefore(newElement, referenceElement);
    ```
    

### 7. 노드 이동

- **방법**: 기존 DOM에서 노드를 제거하고, 새로운 위치에 `appendChild` 또는 `insertBefore`를 사용해 삽입합니다.
- **예시**:
    
    ```jsx
    
    const element = document.getElementById('elementToMove');
    const newParent = document.getElementById('newParent');
    
    newParent.appendChild(element);
    ```
    

### 8. 노드 복사

- **방법**: `Node.prototype.cloneNode(deep)`를 사용해 노드를 복사합니다.
- **사용법**:
    
    ```jsx
    
    const element = document.getElementById('elementToClone');
    const clonedElement = element.cloneNode(true); // true면 하위 노드까지 복사
    
    document.body.appendChild(clonedElement);
    ```
    

### 9. 노드 교체

- **방법**: `Node.prototype.replaceChild(newChild, oldChild)`를 사용해 기존 노드를 새 노드로 교체합니다.
- **사용법**:
    
    ```jsx
    const newElement = document.createElement('div');
    newElement.textContent = '새로운 요소';
    
    const parentElement = document.getElementById('parentId');
    const oldElement = document.getElementById('oldElementId');
    
    parentElement.replaceChild(newElement, oldElement);
    ```
    

### 10. 노드 삭제

- **방법**: `Node.prototype.removeChild(child)` 또는 `Element.prototype.remove()`
- **사용법**:
    
    ```jsx
    
    const parentElement = document.getElementById('parentId');
    const childElement = document.getElementById('childElementId');
    
    parentElement.removeChild(childElement);
    
    // 또는
    childElement.remove(); // 부모 요소에서 자식 요소를 제거
    
    ```
    

### 11. 어트리뷰트

- **속성 설정**: `Element.prototype.setAttribute(name, value)`로 속성을 설정합니다.
- **속성 취득**: `Element.prototype.getAttribute(name)`로 속성을 가져옵니다.
- **속성 제거**: `Element.prototype.removeAttribute(name)`로 속성을 제거합니다.
- **사용법**:
    
    ```jsx
    const element = document.getElementById('myId');
    
    element.setAttribute('class', 'newClass');
    const classValue = element.getAttribute('class');
    element.removeAttribute('class');
    ```
    

### **HTML 어트리뷰트 vs DOM 프로퍼티 🤔**

HTML 어트리뷰트

- HTML 요소의 초기 상태를 지정하는 것이다.
- 즉, HTML 어트리뷰트 값은HTML 요소의 초기 상태를 의미하며 이는 변하지 않는다.

DOM 프로퍼티의 

- 사용자의 입력에 의한 상태 변화에 반응하여 언제나 최신 상태를 유지한다.

### data 어트리뷰트와 dataset 프로퍼티 **🤔**

> Html 요소에 정의한 사용자 정의 어트리뷰트와 자바스크립트 간에 데이터를 교환할 수 있다.
>