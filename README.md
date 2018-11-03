EditComment
===========

Плагин <strong>EditComment</strong> предназначен для включения возможности редактирования сделанных  комментариев.<cut>

Плагин использует нативную для LS 1.0.1 систему комментирования, не требует хаков  темплейтов (при условии следования темплейтами стандартам LS) и, в то же время, обладает гибкостью настройки. Работает с визуальным редактором TinyMCE и плагином Redactorjs.

<strong>EditComment</strong> может хранить "историю" редактирования комментариев заданной вложенности, что может помочь модераторам при рассмотрении жалоб.

Плагин имеет несколько опций, позволяющих ограничивать пользователей в использовании функционала редактирования комментариев:

- ограничение по рейтингу
- ограничение по количеству раз редактирования
- ограничение по времени, прошедшим с момента последнего редактирования
- ограничение на редактирование комментариев, на которые уже есть ответ

Так же могут быть легко добавлены какие-то другие ограничения.

Плагин может добавлять к тексту комментария надпись, сообщающую о дате последнего редактирования.

Имеется возможность задать список пользователей, имеющих право игнорировать ограничения на редактирование комментариев.

Плагин распространяется по лицензии <a href="http://creativecommons.org/licenses/by-sa/3.0/deed.ru">Attribution-ShareAlike 3.0 Unported (CC BY-SA 3.0)</a>
Обязательным условием использования плагина является наличие активной ссылки спонсора оригинальной версии плагина. При модификации плагина запрещается изменять содержание ссылки, а так же помещать ее в невидимые блоки или каким-то образом скрывать ее от людей и роботов поисковиков. Отключить ссылку можно за донейт на сайте <a href="http://livestreetcms.ru/profile/kerby/donate/">http://livestreetcms.ru/profile/kerby/donate/</a>.


Список изменений версий
-----------------------
1.0.4 - незначительные фиксы и поддержка плагина визуального редактора Redactorjs

1.0.3 - фикс в для strict в PHP 5.4

1.0.2 - введены новые опции по использованию истории комментариев и добавлена кнопка отмены редактирования для ясности
Обновление: сохранить свой config/config.php, переписать файлы плагина "поверх", скопировать из нового файла config/config.php в старый файл опции 
```
// Показывать ли кнопку истории редактирования комментария.
// 0 - не показывать никому
// 1 - показывать всем
// 2 - показывать только списку редакторов
// 3 - показывать только админу
$config['show_history_button']=1;

// Показывать ли кнопку отмены редактирования комментария. Можно использовать для "экономии" места под кнопки
$config['show_cancel_button']=true;
```
и переписать в папку конфига. Сбросить кэш.


1.0.1 - исправлен баг с проверкой возможности редактирования топика при AJAX

Замечание по работе плагина
---------------------------

Плагин использует стандартный шаблонный хук comment_tree_end и его наличие в шаблоне обязательно. Если у вас что-то не работае, как, например, в шаблоне lightblue, сначала проверьте наличие этого хука в файле templates/skin/<имя шаблона>/comment_tree.tpl

Он должен стоять в после включения постраничности, т.е. как-то так:

```smarty
{include file='comment_paging.tpl' aPagingCmt=$aPagingCmt}

{hook run='comment_tree_end' iTargetId=$iTargetId sTargetType=$sTargetType}

{if $bAllowNewComment}
  {$sNoticeNotAllow}
```  

Если у вас его нет - вставьте

```smarty
{hook run='comment_tree_end' iTargetId=$iTargetId sTargetType=$sTargetType}
```  