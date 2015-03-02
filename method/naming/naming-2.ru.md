# Соглашение по именованию

БЭМ-методология оперирует понятиями [блоков](), [элементов]() и [модификаторов](). И прежде чем начать с ними работать, необходимо ознакомиться с правилами их именования.

Соглашение по именованию позволяет всегда одинаково называть БЭМ-сущности независимо от того, пишете ли вы CSS, JavaScript или шаблоны, или работаете с файловой системой проекта. Благодаря общей системе вы всегда понимаете из названия, о какой БЭМ-сущности идет речь.

БЭМ-методология задает ряд соглашений и правил по именованию CSS-селекторов(), соблюдение которых решает многие насущные для CSS- верстальщика и веб-разработчика проблемы:

* [Как уменьшить сложность кода?](#)
* [Как начать переиспользоваь код?](#)
* [Как избежать взаимного влияния компонентов друг на друга и упростить рефакторинг?](#)
* [Как понять, о какой конкретно сущности идет речь? Определение всех частей сущности в отрыве от контекста.](#)
* [Как улучшить скорость рендеринга?](#)

В этой статье мы расскажем вам, как простые правила именования БЭМ-сущностей решают все вышеперечисленные проблемы и делают ваш код понятным не только вам, но и другим разработчикам.

### Соглашения об именовании CSS-селекторов

Основная идея соглашения об именовании CSS-селекторов — сделать их более понятными и научиться различать блоки, элементы и модификаторы только по их именам.

Рассмотрим простой CSS-селектор `menuitemvisible`. Такую запись сложно вопринимать особенно при быстром просмотре. Напрашивается добавление какого-нибудь разделителя, например, `menu-item-visible` или `menuItemVisible`. В таком виде имя селектора становится намного понятнее за счет явного выделения логических частей: отдельные имена легко вычленить из общей записи и достаточно легко предположить, что `menu` в данном случае, скорее всего, окажется блоком, `item` — элментом, а `visible` — модификатором. В таком простом примере все очевидно, однако жизненные ситуации зачастую намного сложнее и не столь однозначны.

Методология БЭМ использует жесткие правила именования CSS-селекторов, которые помогают не только легко отделять имена сущностей друг от друга, но и со стопроцентной точностью определять тип БЭМ-сущности только по ее имени.

БЭМ использует CSS-классы для хранения информации о блоках, элементах и модификаторах.

<!-- Канонический стиль соглашения об именовании CSS-селекторов, предложенный методологией БЭМ, позволяет со стопроцентной точностью определить тип БЭМ-сущности по ее имени.
 -->
 Приведенные в данном разделе правила и примеры основаны на каноническом стиле именования, однако он не исключает наличия [альтернативных схем](#name-scheme), более подходящих вам или вашему проекту.

#### Имя блока

Имя блока формируется как `имя-блока-из-нескольких-слов`.

Имя блока служит [неймспейсом](https://ru.wikipedia.org/wiki/Пространство_имён) для его елементов и модификаторов.

**Примеры**

`lang-switcher`

`button`

`menu`

> ОФОРМИТЬ КАК ВРЕЗКУ
>##### Использование префиксов в именах блоков

>Иногда для большей информативности и простоты восприятия кода в имена блоков могут добавляться различные префиксы.

>Так, исторически сложившейся традицией в БЭМ было использование префикса `b-` (от `block`) для обозначения блока с визуальным представлением. А префикс `i-` или `js-` (от `include` и `javascript`) означал, что блок не имеет визуальной реализации и является вспомогательным для построения других блоков. Но так как сейчас большая часть блоков имеет JS-представление, то уже нет необходимости отличать технологии реализации блока на уровне имен.

>**Пример**

>`b-link`

#### Имя элемента

Имя элемента формируется также, как и имя блока `имя-элемента-из-нескольких-слов`.

Для определения принадлежности элемента к блоку, мы добавляем неймспейс в виде имени блока и отделям его двумя подчеркиваниями. Полное имя элемента создается по схеме:

`имя-блока__имя-элмента`

**Пример**

`lang-switcher__item`

`menu__item`

`table__row`

Если блок имеет несколько одинаковых элементов, как в случае пунктов меню, то все они будут иметь одинаковое имя.

_________________________________________

**Важно помнить!** В методологии БЭМ не существует элементов элементов.

Неймспейсом служит только имя блока. Отражать вложенность в именах элементов не имеет смысла, так как это не позволит легко вынуть один элемент из другого при повторном использовании блока в другой ситуации (или при рефакторинге).

>Неверно

```
nav/
    __item/
        nav__item.css
    __link/
        nav__link.css
```

Для выражения вложенности вполне достаточно DOM-дерева:

>Верно

```html
<ul class="nav">
    <li class="nav__item">
        <a class="nav__link"></a>
    </li>
</ul>
```

#### Имя модификатора

Имя мододификатора формируется как `имя-модификатора-из-нескольких-слов_имя-значения-из-нескольких-слов`.

Модификаторы бывают булевыми (например, `visible : true`) или представляют собой пару «ключ — значение» (`size : large`, `type : search`). Модификаторы чем-то похожи на атрибуты в HTML.

Значение булевого модификатора в его имени не указывается. Так имя модификатора `visible : true` будет записано, как `visible`.

В модификаторах типа «ключ — значение» имя отделяется от значения одним подчеркиванием, `size_large`.

Модификаторы с одинаковыми именами могут принадлежать как блокам, так и элементам и оказывать на них различное воздействие. Поэтому для определения принадлежности модификатора к его «владельцу», необходимо добавлять неймспейс в виде имени блока или имени блока и его элемента.

Полное имя модификатора создается по схеме:

* Для булевых модификаторов<br>
    `имя-владельца_имя-модификатора`
* Для модификаторов вида «ключ-значение»<br>
    `имя-владельца_имя-модификатора_значение-модификатора`

##### Модификатор блока

Булевый: `имя-блока_имя-модификатора`.

Вид «ключ – значение»: `имя-блока_имя-модификатора_значение-модификатора`.

**Пример**

`lang-switcher_disabled`

`menu_type_radio`

##### Модификатор элемента

Булевый: `имя-блока__имя-элемента_имя-модификатора`.

Вид «ключ – значение»: `имя-блока__имя-элемента_имя-модификатора_значение-модификатора`.

**Пример**

`lang-switcher__item_visible`

`table__box_align_top-left`

### Дополнительные правила БЭМ-нотации Основные положения соглашения по именованию методологии БЭМ

#### Не используем селекторы, кроме селекторов класса

БЭМ-методология



#### Не используем каскад




#### Не используем id.

#### Не используем вложенность элементов.


## От проблем к решениям (Страхи веб-разработчиков)

Этот раздел документа посвящен основным проблемам, с которыми сталкиваются и CSS-верстальщики и веб-разработчики, и их решениям с помощью соглашения об именовании в методологии БЭМ.

### Как уменьшить сложность кода в современном фронтенде?

Распространенная ситуация: вы разрабатываете свой проект, называете, казалось бы, очевидные вещи своими именами. Вам понятно, какие компоненты интерфейса для чего служат и за что отвечают.

<ul class="nav">
    <li class="item active"><a class="link">One</a></li>
    <li class="item"><a class="link">Two</a></li>
    <li class="item"><a class="link">Three</a></li>
</ul>

У вас есть вполне понятные и прозрачные CSS-правила к каждому классу, например:

```
.item
{

}

.active
{

}
```

> Проблема

Пока вы работаете со страницей или проектом, вы помните и понимаете, какие компонетны используют класс `active`. И если проект относится к типу «сделал-отдал-забыл», то такой вид нотации вполне приемлим. Но если вам придется его поддерживать, то вернувшись к коду через пару месяцев, вы вряд ли сразу вспомните, на что могут повлиять правила данного селектора. Чтоб разобраться, можно ли их безболезненно поменять, вам придется просмотреть всю структруру страницы или даже проекта (если вы переиспользовали данное правило).

Вполне может оказаться, что у вас существует еще и такой вариант использования класса `active`:

```
<div class="snippets">
    <div class="item">
        <div class="active">
            <div class="title"></div>
            <img class="thumb" />
        </div>
    </div>
</div>
```

И прописанные к нему CSS-правила:

```
.snippets .active
{

}
```

А теперь представьте такую же ситуацию с большим проектом — любое изменение потребует огромных временных затрат для его тщательного изучения.

Практически каждый разработчик согласится, что пока вы справляетесь с тем количеством данных, которые можно удержать в голове, вы можете успевать вовремя все менять. Но как только вы переключаетесь на другой проект или в вашем приложении добавляется еще десяток страниц, код становится сложно поддерживать.

> Решение

Используя БЭМ, вы будете сразу видеть четкие связи между компонентами. Рассмотрим этот же пример, но уже с примененными правилами именования БЭМ-методологии: селектор `nav` будет означать имя блока, селектор `nav__item` — имя элемента, а `nav__item_active` — имя его модификатора. В таком случае запись будет следующей:

```
<ul class="nav">
    <li class="nav__item nav__item_active"><a class="link nav__link">One</a></span></li>
    <li class="nav__item"><a class="link nav__link">Two</a></li>
    <li class="nav__item"><a class="link nav__link">Three</a></li>
</ul>
```

И, соответственно, CSS будет иметь такой вид:

```
.nav__item
{

}

.nav__item_active
{

}
```

Имена CSS-классов в таком случае информативны достаточно, чтобы вам не пришлось заглядывать в HTML-код страницы. Имя селектора всегда будет содержать знания о том, что данные правила влияют только на модификацию конкретного блока или его элемента (в данном случае элемента `nav__item`). И вам не придется думать о `.snippets .active`, так как его CSS-правила будут записаны как `snippets__item_active` и не будут зависеть от правил модификатора `active`, относящегося к другой БЭМ-сущности.

Как результат применения правил по именованию, предложенных БЭМ-методолгией, вы:

* задаете четкие связи между разными сущностями;
* определяете типы сущностей по их именам;
* упрощаете восприятие вашего кода (имена CSS-классов достаточно просты для восприятия).

Помимо всего вышеперечисленного, использование методологии БЭМ дает вам возможность получить **самодокументируемый код** вашего проекта.

#### Самодокументируемый код





Когда вы пишете веб-приложение, состоящее всего из нескольких страниц, вы можете контролировать то ограниченное число классов, с которым вам приходится работать. Пока вы справляетесь с тем количеством данных, которые можно удержать в голове, вы можете успевать вовремя все менять. Но как только вы переключаетесь на другой проект или в вашем приложении добавляется еще десяток страниц, код становится сложно поддерживать.

> Проблема

У вас отличный живой большой проект, который надо совершенно немного подкорректировать, изменив, допустим, иконки в списки меню. Кажется, это достаточно легко сделать

.menu .item
{

}

Однако, в большом проекте велика вероятность того, что какой-то компонент также опирается на стили, описанные в `.menu .item`, но вспомнить все варианты употребления пунктов меню в вашем проекте просто невозможно. Поэтому, изменения правил одного селектора повлекут за собой изменения в «неожиданных» частях вашего проекта.















### Без контекста непонятно, какой компонент интерфейса описан в классе.

Когда вы разрабатываете свой проект, вы называете, казалось бы, очевидные вещи своими именами, вам понятно, какие компоненты интерфейса вы используете и за что они отвечают.

<ul class="nav">
    <li class="item"><span class="active"><a class="link">One</a></span></li>
    <li class="item"><a class="link">Two</a></li>
    <li class="item"><a class="link">Three</a></li>
</ul>

У вас есть вполне понятные и прозрачные CSS-правила к каждому классу, например:

.item
{

}

.active
{

}

> Проблема

Пока вы работаете со страницей или проектом вы помните и понимаете, какие компонетны используют класс `active`. И если проект относится к типу «сделал-отдал-забыл», то такой вид нотации вполне приемлим. Но если вам придется его поддерживать, то вернувшись к коду через пару месяцев, вы вряд ли сразу вспомните, на что могут повлиять правила данного селектора. Чтоб разобраться, можно ли их безболезненно поменять, вам придется просмотреть всю структруру страницы или даже проекта (если вы переиспользовали данное правило). А теперь представьте такую же ситуацию с большим проектом — любое изменение потребует тщательного изучения проекта.

> Решение

Используя БЭМ, вы будете сразу видеть четкие связи между компонентами. Рассмотрим этот же пример через призму БЭМ-методологии: селектор `item` будет обозначть имя блока, а селектор `active` являться модификатором этого блока. В таком случае запись будет следующей:

<ul class="nav">
    <li class="item item_active"><a class="link">One</a></span></li>
    <li class="item"><a class="link">Two</a></li>
    <li class="item"><a class="link">Three</a></li>
</ul>

И, соответственно, CSS будет иметь такой вид:

.item
{

}

.item_active
{

}

CSS будет информативен достаточно, чтобы вам не пришлось заглядывать в HTML-код страницы. Имя селектора всегда будет содержать знания о том, что для данные правила влияют только на модификацию конкретного блока (в данном случае блока `item`).

### Меняем CSS-правила одного компонента страницы и при этом не ломаем другие. Реальность или миф?

В стандарнтой веб-разработке это скорее миф.

Описывая страницу, вы зачастую оперируете одними и теми же понятиями: всевозможные пункты (`item`) могут встречаться в совершенно различных ситуациях, ссылок на странице может быть множество, при этом какие-то из них должны уводить читателя на другую страницу, какие-то просто облегчать навигацию по странице.

Так, если у вас на странице будет такой код:

<ul class="nav">
    <li class="item"><a class="link">One</a></li>
    <li class="item"><a class="link">Two</a></li>
    <li class="item"><a class="link">Three</a></li>
</ul>

То CSS-стили к пункту `item` скорее всего будут записаны так:

.item
{

}

В случае, если на страницу будет необходимо добавить еще какие-то компоненты, состоящие из пунктов, например:

<div class="snippets">
    <div class="item">
        <div class="title"></div>
        <img class="thumb" />
    </div>
</div>

То веротность того, что CSS-правила будут оформлены с помощью каскада возрастает. Не зря ведь CSS назван Cascading Style Sheets.

.item
{

}

.snippets .item
{

}

Такой подход кажется вполне удобным и логичным: вы просто доопределяете правила, написанные для `item`.

> Проблема

И страница может совршенно безболезненно так существовать и работать до тех пор, пока вы или менеджер проекта не захотите отрефакторить страницу, переместить какие-то пункты меню, использовать написанный код в другом месте отдельно от родителя.

Как только вам понадобится выполнить какое-то из вышеперечисленных действий, вы столкнетесь с проблемой того, что казалось бы независимые части вашего кода слишком связаны и влияют друг на друга. Вы не можете исправить какой-то один компонент, не зацепив так или иначе стили друго. В такой ситуации, желая изменить один компонент, вам придется корректировать или полностью переписывать стили всех зависимых от него компонентов, много копировать, удалять или вообще отменять стили.

Изменив стили для одного компонента страницы, вы можете получить неожиданный «сюрприз» в виде сломанного зависимого компонента.

> Решение

Опираясь на соглашения по именованию CSS-селекторов в БЭМ, у вас всегда будет возможность внести изменения точечно, не ломая зависимые компненты. В БЭМ каждый класс имеет уникальное имя и является самодостаточным.

Запишем привденный в пример код в соответствии с правилами именования БЭМ:

<ul class="nav">
    <li class="nav__item"><a class="link nav__link">One</a></li>
    <li class="nav__item"><a class="link nav__link">Two</a></li>
    <li class="nav__item"><a class="link nav__link">Three</a></li>
</ul>

В таком случае CSS для пункта в списке `nav` будет независим от CSS-правил для самого `nav`:

.nav
{

}

.nav__item
{

}

А добавляя на страницу дополнительные пункты, вы также назовете их, ориентируясь на контекст:

<div class="snippets">
    <div class="snippets__item">
        <div class="snippets__title"></div>
        <img class="snippents__thumb" />
    </div>
</div>

.snippets__item
{

}

Внесенные изменения в `nav` никогда не будут влиять на элемент `nav__item`, а изменения `nav__item` никак не отобразятся на пункте `snippets__item`. Прозрачное именование блоков, элементов и модификаторов и уход от каскадов позволят вносить изменения только в конкретные кмпоненты и иметь четкое представление, к какому блоку относится каждый элемент и какие стили могут на него влиять.

### Скорость рендеринга и селекторы большой вложенности в CSS

Как уже говорилось выше применение каскада в CSS вполне оправдано в случае стандартного подхода к разработке, но использование селекторов большой вложенности может значительно снизить быстродействие вашего сайта.

Конечно, на маленьких и средних страницах CSS не может сильно влиять на скорость. Однако, если ваш проект растет (а большинство разработчиков стремятся именно к этому), вы уже не можете не учитывать этот фактор, влияющий на скорость. К тому времени, когда вы осознаете, что CSS замедляет работу проекта, будет очень сложно или практически невозможно начинать оптимизацию CSS-правил.

Решение

Правила именования в БЭМ созданы таким образом, что каждый БЭМ-класс имеет уникальное имя и является самодостаточным – разные блоки никогда не пересекаются по именам классов.

Это означает, что вам, скорее всего, достаточно указать один класс, чтобы:

* описать стили самого блока;
* описать стили любого элемента внутри блока;
* добавить дополнительные стили или переопределения с помощью модификатора.

Большинство браузеров начинают применять селектор с «правой части» (охватывающей чаще всего большее множество узлов) и затем уточняют полученную выборку, фильтруя ее применением оставшихся правил. Чем больше шагов фильтрации требуется, тем больше времени это занимает. Современные браузеры очень хорошо оптимизированы для этих задач, но последние версии установлены далеко не у всех, и мобильные устройства всегда могут вести себя иначе — а селекторы, состоящие из одного класса, как минимум относятся к самым быстрым селекторам из всех возможных.

Конечно же БЭМ не отменяет каскад в CSS! Однако он значительно сокращает его использование. Существуют сложные случаи, когда необходимо указать два и более классов в одном селекторе. Например, сочетание модификаторов, внутренние зависимости элементов или влияние модификатора блока на стили отдельных его элементов:

```
.menu-item_disabled .menu-item__label
{
   display: none;
}
```

Но поскольку БЭМ превращает CSS из простого набора классов в семантическую модель проекта, то скорее всего потребность переопределить заданные стили будет зависеть от модификатора, который, как и положено в БЭМ, будет иметь свою уникальное имя. Таким образом нам удается сохранить специфичность CSS-правил.



### Как писать код, который можно переиспользовать?

Можно с уверенностью сказать, что все интерфейсы абсолютно разные. Однако, также уверено можно заявлять и о том, что все интерфейсы состоят и одних и тех же компонентов: все испольуют кнопки, поля для ввода, списки и ссылки. Только выглядят эти компоненты все совершенно по-разному, а принципиальных отличий в поведении практически нет. Именно поэтому большинство разработчиков так хотят использовать уже написанный код на разных страницах и проектах. Согласитесь, зачем даже на одной странице каждый раз описывать кнопку заново, если они отличаются только стилями.

> Проблема

Рассмотрим все тот же блок кода:

<ul class="nav">
    <li class="item item_active"><a class="link">One</a></span></li>
    <li class="item"><a class="link">Two</a></li>
    <li class="item"><a class="link">Three</a></li>
</ul>

.item
{

}

.item .link
{

}

У вас есть отличный список со ссылками, подходящий для вашего следующего проекта. Однако, чаще всего вы не можете просто вязть нужный вам кусок кода и вставить на новое место, большинство стилей сломаются из-за использования каскада. Так, ваши пункты меню скорее всего будут опираться на стили для `.item`, который тоже нужно будет перенести в новый проект, либо придется дополнять правила для переиспользуемого блока.

> Решение

Разбивая код на логически независимые части (блоки), вы создаете кубики для конструктора, которые легко перемещать в пределах одной страницы, переносить на другие страницы или в другие проекты.

Независимость блоков касается не только CSS. В методологии БЭМ блок является абсолютно независимой и самодостаточной единицей. Он знает о себе все: свой внешний вид (CSS), поведение (JavaScript и шаблоны) и перечень блоков, с которыми ему необходимо взаимодействовать (зависимости).

Уникальность имен классов, основанное на правилах именования БЭМ, позволяет блокам не зависеть друг от друга.

### Рефакторинг

Основные проблемы рефакторинга в совренеменном веб-проекте:

* найти тот код, который хочется что-то поменять;
* починить и при этом не сломать зависимые компоненты.



<a name="name-scheme"></a>
### Распространенные схемы именования по БЭМ

**Классический стиль**

`block-name__elem-name_mod-name_mod-val`

Использование описано в предыдущей главе. Данный стиль имеет один существенный плюс – все предлагаемые инструменты [платформы БЭМ](), в том числе и с открытыми исходниками, ориентируются именно на такое именование.

**Стиль Гарри Робертса**

`block-name__elem-name--mod-name`

* использование дефиса в именах;
* отделение имени элемента от блока с помощью двух подчеркиваний;
* отделение булевых модификаторов с помощью двух дефисов;
* модификаторы вида «ключ-значение» не используются.

**Стиль без подчеркиваний**

`blockName-elemName--modName-modVal`

* использование в именах «верблюжего регистра»;
* отделение имени элемента от блока с помощью одного дефиса;
* отделение модификаторов с помощью двух дефисов;
* отделение значения модификатора с помощью одного дефиса.
