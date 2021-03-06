# metaprogramming {#meta}

еще один мощный способ программирования на Python – метапрограммирование

> Метапрограммирование — вид программирования, связанный с созданием программ,
> которые порождают другие программы как результат своей работы (в частности,
> на стадии компиляции их исходного кода), либо программ, которые меняют себя
> во время выполнения (самомодифицирующийся код).

* https://www.youtube.com/watch?v=QKFrxEkVusg
* https://www.youtube.com/watch?v=bt6kU1kuHWA

Традиционно при написании программ стараются писать код максимально переносимым
между различными компиляторами. ОС и аппаратурой, для этого создают различные 
фреймворки, HAL, стандартные библиотеки и т.п. В итоге вместо быстрых эффективных 
программ получаются **Jаба**троны завернутые в сотни слоев абстракций и выжирающих
ОЗУ гигабайтами (Eclipse на запуске на пару минут вырубает не самый тухлый i7).

Метапрограммирование на metapy решает обратную задачу: получение исходного кода
на embedded C (*) максимально учитывающего все особенности используемой
аппаратуры, окружения и конкретной решаемой задачи. Общая идея -- 
* шаблонизация, 
* параметризация и 
* наследование исходного кода

написанного на языках программирования,
которые в принипе не знают об ООП, наследовании и шаблонах (ANSI C, Makefile,
МЭК 61131-3) или не способных их полноценно реализовать (**). Вся абстрактная
каша должна оставаться на рабочей станции разработчика в высокоуровневом
Python-коде, результат -- низкоуровневый код на Си/LLVM способный работать на
сотнях байт ОЗУ.

Идеальным результатом применения metapy будет код, не выполняющий ни одной машинной
инструкции, которая не является необходимой для инициализации конкретной железки,
или решения текущей задачи. Если код должен работать поверх ОС, в идеале он
должен использовать только нативное API и 
* специфицированный код

вместо сторонних библиотек и особенно мультиплатформенных фрейморков. В реальности
естественно приходится ограничиваться точечным применением, т.к. есть legacy код,
требования к читаемости выходного кода, обучение программистов сложной методике, 
сложность реализации вывода (компиляция мета-моделей), и невозможность переписать
в виде метамоделей весь используемый набор сервисов и библиотек.

(*) C++, Java или любом другом языке, в т.ч. на Python для самораскрутки системы

(**) интерересно через сколько десятилетий наконец додумаются встроить в
компилятор C++ интерпретатор (Лиспа?) для построения кода в compile time, вместо 
шизоидных шаблонов?
