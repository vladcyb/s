# Блок 1

## 1. Почему ['R'] === ['R'] === false?

Сравнение на равенство двух неприметивных всегда возвращает **false**.

## 2. Плюсы использования const

Плюсы использования **const/let** в отличии от **var**

- Область видимости — блок. У **var** область видимости функция.

Пример:

```js
function test() {
  let a = 123

  for (let i = 0; i < 1; i++) {
    let a = 0
    console.log(a)
  }

  console.log(a)
}

test()
```
Выведет в консоль 0, потом 123, так как создались две разые переменные, каждая в отдельной области видимости.

- Если вызвать переменную, объявленную через **const/let** до ее создания, то возникнет ошибка (которая будет видна в консоли), что позволит найти ошибку в коде на более раннем этапе разработки.
- При использовании в цикле, для каждой итерации создаётся своя переменная.

Пример:
```js
function makeArmy() {

  let shooters = []

  for (let i = 0; i < 10; i++) {
    shooters.push(function () {
      console.log(i)
    })
  }

  return shooters
}

const army = makeArmy()

army.forEach((item) => {
  item()
})
```
В консоль выведутся числа от 0 до 9, так как для каждой итерации создаётся своя переменная и, как следствие, на каждой итерации произойдет замыкание для переменной i в функцию, которая добавляется в массив.

**const** в отличии от **let** не позволяет изменять переменную, что позволяет допустить меньше ошибок в коде.

## 3. Что отработает быстрее - setTimeout или Promise. И почему?

Промисы создают микрозадачи, а setTimeout макрозадачи. Микрозадачи выполняются раньше макрозадач. Следовательно, то, что было в обработчике промиса, выполнится раньше, чем то, что было в setTimeout.

## 4. Как прочитать http-only куки?

Только на сервере. Либо в инструментах разработчика.

## 5. Назовите 4 способа применить стили на компонент

- CSS
- Inline-стили
- styled-components
- CSS-модули

## 6. Как предотвратить лишние рендеры у функциональных компонентов?

- Обернуть в memo
- При необходимости обернуть в useCallback и в useMemo передаваемые пропсы
- Создавать стейт и вызывать контекст как можно ниже в дереве компонентов (только там, где они нужны), чтобы лишние рендеры не происходили в компонентах, в которых этот стейт или контекст не используется.

## 7. Минусы использования Context API
- При обновлении значений в контексте происходит рендер всех компонентов, лежащих ниже провайдера контекста в иерархии компонентов.
- Можно нечаянно обратиться не к тому провайдеру (в случае, если компонент обернут в провайдер одного и того же контекста несколько раз)

# Блок 2
asdadas
1. Create React App устарел.
2. Пришлось установить npm-пакет uuid.
3. Не грузить иконки отдельным запросом.
4. Не создавать модалку в каждом элементе списка.
5. Использовать clsx или подобную библиотеку для динамических CSS-классов.
6. Выносить модалку за корневой элемент при помощи портала.
7. https://github.com/surfstudio/frontend-interview-test_todo/blob/0f34efeac13406ca6ebdba36ef2ed6d96ea2e504/src/Modal/ModalCreateItem.tsx#L66.  
   Нечитаемый код. Вынести в функцию. Кроме того, здесь баг.


```typescript
    name
    ? () => {
        dispatch(
          isCategories
            ? categoriesAdded({ name, description })
            : tasksAdded({
                name,
                description,
                category: setSelected, // баг
              })
        );
        clearState();
        setActive(false);
      }
    : () => {}
```

Как можно было написать:

```typescript
const onSubmit = () => {
  if (!name) {
    return;
  }

  dispatch(
    isCategories
      ? categoriesAdded({ name, description })
      : tasksAdded({
        name,
        description,
        category: selected, // selected вместо setSelected
      })
  );
  clearState();
  setActive(false);
}
```

8. https://github.com/surfstudio/frontend-interview-test_todo/blob/0f34efeac13406ca6ebdba36ef2ed6d96ea2e504/src/Lists/ListItem.tsx#L55  
   Обновлять стейт нужно через сеттер.

9. Не добавлять модалку в DOM-дерево, если она закрыта.
10. Убирать скролл при открытой модалке.
11. Не задавать фиксированную высоту для **list-item**, так как в нем может быть много текста.
12. Добавить для класса **list-item-col2** правило **flex-shrink: 0;**, чтобы кнопки всегда отображались горизонтально.
13. Если в открытой модалке зажать левую кнопку мышки в текстовом поле, а затем перенести курсор вне модалки и отпустить мышку, то модалка закроется. Нужно это исправить для лучшего UX. Например, убрать вообще функцию закрытия при нажатии за модалку.
14. Лучше называть редьюсеры в виде **add**, **update**, **remove**.
15. Если перейти на несуществующую страницу, то можно создавать задачу, но список при этом останется пуст. Это вводит в заблуждение. Либо делать редирект на страницу задач, либо не отображать хедер на несуществующей странице.
16. Тесты не должны быть в src
17. 
