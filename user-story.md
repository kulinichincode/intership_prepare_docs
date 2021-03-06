# User story

> ## Application name

`lunch-menu`

---

> ## Description

Приложение предназначено для формирования и учета заказов обедов в офисе.
С помощью приложения пользователи могут выбирать из предложенного меню набор блюд на обед. Пользователь-администратор приложения осуществляет ввод меню на предстоящий день, ввод значения баланса денег на счетах пользователей после получения от них наличной оплаты, формирует с помощью приложения сводный заказ на доставку обедов в офис. Пользователи имеют возможность видеть баланс своего счета, историю своих заказов. Информация о блюдах, входящих в меню обеда, отображается в виде текста и фотографий.

---

> ## Pages

При открытии сайта проверяется, вошел пользователь в систему или нет. Если пользователь вошел, то идет перенаправление на `Home page`. Если пользователь не вошел, то идет перенаправление на Signin page.

1.  ### `Signin page` - страница входа в приложение.

    На этой странице отображаются поля ввода `Email`, `Password` и кнопка `Sign in`.
    Ниже кнопки `Sign in` находится ссылка перехода на страницу регистрации `Signup page`.
    По нажатию на кнопку `Sign in` отправляется запрос на backend. Если `email` и `password` правильно введены, то backend возвращает `JWT`, который в дальнейшем используется для запросов к backend. Если `email` и `password` не правильно введены, то backend возвращает ответ с указанием на ошибку и на странице `Signin page` показвается сообщение об ошибочном вводе. После получения `JWT`, он сохраняется в local storage, а затем идет перенаправление на страницу `Home page`.

2.  ### `Signup page` - страница регистрации в приложении.

    На этой странице отображаются поля ввода `Email`, `Password`, `Repeat Password` и кнопка `Sign up`.
    Ниже кнопки `Sign up` находится ссылка перехода на страницу входа в приложение `Signin page`.
    По нажатию на кнопку `Sign up` отправляется запрос на backend. Backend формирует письмо, с однократным кодом регистрации и отправляет его на указанный email. Пользователь открывает в почтовом клиенте письмо и нажимает на ссылку в письме с кодом регистрации. Ссылка ведет на frontend на страницу `Email verification page`.

3.  ### `Email verification page` - страница проверки email при регистрации в приложении.

    На этой странице отображаются поля ввода `Email` без возможности редактирования, скрытое поле с кодом регистрации и кнопка `Verify email`.
    Ниже кнопки `Verify email` находится ссылка перехода на страницу входа в приложение `Signin page`.
    По нажатию на кнопку `Verify email` отправляется запрос на backend с email и кодом регистрации. Backend проверяет email и код регистрации, и в случае успеха возвращает JWT. Далее действия производятся аналогично `Signin page`. Если ответ от backend отрицательный, то выдается сообщению пользователю об ощибке проверки email.

4.  ### `Home page` - основная страница приложения.

    На основной странице отображается перечень обеденных наборов с возможностью выбрать один из них. Перечень обеденных наборов загружается с backend.
    В backend существует два состояния:

    - режим выбора меню, данные о меню доступны пользователю, возвращается список наборов меню;
    - режим ввода меню, данные о меню пользователю не доступны, возвращается пустой список.

    Переключение режимов выбора обеденных наборов осуществляет пользователь-администратор на странице `Admin page`.
    В верхней части `Home page` отображается пункты меню. в котором показано на какой странице находится пользователь. Нажимая на пункты меню, пользователь осуществляет навигацию по страницам. Для пользователя-администратора кроме всех остальных страниц доступна страница `Admin page`.

    Перечень страниц в меню:

    - `Home`;
    - `Statistics`;
    - `Admin`.

    Каждый обеденный набор отображается в виде списка, в котором справа от фотографии блюда отображается текстовое описание блюда. Пользователь выбирает один из наборов в который входит несколько блюд путем нажатия на весь набор. При этом информация о выборе пользователя отправляется на backend. При первоначальной загрузке страницы 'Home page' с backend передаются данные о выборе пользователя и соответсвующий выбор отображается с помощью рамки вокруг выбранного обеденного набора блюд.

    В верхнем правом углу отображается баланс пользователя и кнопка `Sign out`. При нажатии на кнопку `Sign out` осуществляется сброс состояния текущего пользователя и JWT, и идет перенаправление на страницу `Sign in page`.

5.  ### `Statistics page` - страница истории выбора пользователем обеденных наборов.

    На странице отображается с возможностью pagination таблица обеденных наборов, которые ранее выбирал пользователь.
    Наименование колонок таблицы:

    - `Дата`;
    - `Номер обеда`;
    - `Описание обеда`;

    В верхней части `Statistics page` отображается пункты меню. в котором показано на какой странице находится пользователь. Нажимая на пункты меню, пользователь осуществляет навигацию по страницам. Для пользователя-администратора кроме всех остальных страниц доступна страница `Admin page`.

    Перечень страниц в меню:

    - `Home`;
    - `Statistics`;
    - `Admin`.

    В верхнем правом углу отображается баланс пользователя и кнопка `Sign out`. При нажатии на кнопку `Sign out` осуществляется сброс состояния текущего пользователя и JWT, и идет перенаправление на страницу `Sign in page`.

6.  ### `Admin page` - страница для пользователя-администратора.

    На странице отображаются:

    - переключатель режима выбора меню;
    - четыре набора меню с возможностью добавления/удаления отдельных блюд;
    - таблица пользователей с отображением и возможностью ввода баланса каждого пользователя;
    - кнопка формирования заказа.

    Если переключатель режима выбора меню в состоянии `включено`, то заблокировано редактирование наборов меню. Если переключатель режима выбора меню в состоянии `выключено`, то редактирование наборов меню разрешено.

    По нажатию на кнопку формирования заказа, появляется модальное окно с таблицей заказа, со следующими колонками:

    - `Номер обеда`;
    - `Количество обедов`.

    В верхней части `Admin page` отображается пункты меню. в котором показано на какой странице находится пользователь. Нажимая на пункты меню, пользователь осуществляет навигацию по страницам. Для пользователя-администратора кроме всех остальных страниц доступна страница `Admin page`.

    Перечень страниц в меню:

    - `Home`;
    - `Statistics`;
    - `Admin`.

    В верхнем правом углу отображается баланс пользователя и кнопка `Sign out`. При нажатии на кнопку `Sign out` осуществляется сброс состояния текущего пользователя и JWT, и идет перенаправление на страницу `Sign in page`.
