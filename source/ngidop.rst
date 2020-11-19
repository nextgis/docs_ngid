.. sectionauthor:: Роман Гайнуллов <roman.gainullov@nextgis.com>

.. _ngidop:

Общее описание
==============

NextGIS ID on-premise (NGID on-premise) - это сервер авторизации и управления пользователями программного обеспечения NextGIS. 
В локальных сетях организаций с определенным уровнем изоляции от глобальной сети интернет, требуются функции авторизации пользователей настольного 
и мобильного программного обеспечения (ПО) NextGIS.

NGID on-premise предоставляет следующие возможности:

* вход пользователей с указанием логина и пароля;
* изменение свойств пользователей (имя, пароль), удаление пользователей;
* добавление пользователей в команду, которой обеспечивается расширенный доступ к функциональности ПО, изменение состава команды;
* авторизация пользователей через OAuth2 в различных приложениях;
* персональная веб страница пользователя с профилем пользователя и возможность изменить пароль входа.

.. _ngidop_auth:

Вход и профиль
--------------

При переходе на главную страницу NGID on-premise открывается диалог входа пользователя (см. :numref:`auth_window`), в котором необходимо указать логин и пароль пользователя, заведенного в административном интерфейсе.

.. figure:: _static/auth_window.png
   :name: auth_window
   :align: center
   :width: 16cm

   Окно авторизации пользователя

После успешной авторизации, пользователю отображается окно со страницей его профиля (см. :numref:`profile_window`). 
В данном окне пользователь может изменить информацию о себе и пароль учетной записи.

 
.. _ngidop_teams:

Команда
--------

Механизм управления командой позволяет добавить в свою команду дополнительного пользователя, указав для него логин и пароль, или удалить его из команды. Управление командой доступно через личный кабинет по подпути **/users** в разделе “Команда” (см. :numref:`ngidop_team`). Каждый добавленный пользователь появится в списке и будет иметь расширенный доступ к функиям ПО NextGIS.

.. figure:: _static/ngidop_team.png
   :name: ngidop_team
   :align: center
   :width: 16cm

   Добавление пользователей в Команду


.. _ngidop_app_oauth:

Приложения OAuth
-----------------------

В разделе *Приложения OAuth* предоставляется доступ для авторизации в различных приложениях NextGIS - `NextGIS Formbuilder <https://docs.nextgis.ru/docs_formbuilder/source/gui.html#ngidop>`_, `NextGIS QGIS <https://docs.nextgis.ru/docs_ngqgis/source/auth.html#ngidop>`_, NextGIS Web, NextGIS Collector, `NextGIS Mobile <https://docs.nextgis.ru/docs_ngmobile/source/auth.html#ngidop>`_ (см. :numref:`ngidop_apps_oauth`).

Каждое из этих приложений можно быть настроено для авторизации через NextGIS ID on-premise. По умолчанию эти приложения авторизуются через my.nextgis.com - облачный сервис. Подробности о том, как настроить авторизацию в этих приложениях см. в их документации.

.. figure:: _static/ngidop_apps_oauth.png
   :name: ngidop_apps_oauth
   :align: center
   :width: 16cm

   Настройка OAuth applications

.. _ngidop_ldap:

Настройка LDAP
--------------

Страница настроек LDAP открывается по подпути **/ldapsettings** (см. :numref:`ldap_settings`).
В блоке LDAP SERVER указывается адрес сервера авторизации, логин/пароль учетной записи пользователя для подключения к серверу.

**Примечание: интеграция с внешним сервером Microsoft Active Directory.** 
При авторизации через стандартный диалог входа NextGIS Web идет проверка существования данного пользователя в ПО NextGIS Web. Если аккаунт пользователя имеет тип Microsoft Active Directory - то проверка пароля осуществляется в Microsoft Active Directory. Если пользователя не существует, то проверяется существование пользователя в сервере Microsoft Active Directory. Если пользователь существует, то проверяется введенный пароль. Если сервер Microsoft Active Directory успешно авторизовал пользователя, то в ПО NextGIS Web создается пользователь с такими же логином и именем и типом аккаунта Microsoft Active Directory.

.. figure:: _static/ldap_settings.png
   :name: ldap_settings
   :align: center
   :width: 16cm

   Страница настроек LDAP
   
В блоке **Поиск пользователя** указывается база, в которой осуществляется поиск пользователя и его LDAP атрибуты, соответствующие искомым параметрам (логин, имя, фамилия).

Если пользователь принадлежит какой-то **группе**, то имеется возможность указать это в последнем блоке настроек конфигурации LDAP. Параметр не является обязательным, но дает возможность ограничивать авторизацию пользователей, не принадлежащих к конкретной группе. Пользователи из других групп не будут иметь возможности авторизоваться даже при указании корректной пары логин/пароль.

.. _ngidop_guids:

Идентификатор NextGIS ID on-premise
-----------------------------------

Для интеграции с глобальными сервисами NextGIS (такими как `geoservices <https://geoservices.nextgis.com/>`_, `NGQ Rosreestr Tools <https://docs.nextgis.ru/docs_ngqgis/source/NGQ_Rosreestr_Tools.html?highlight=ngq>`_) используется уникальный GUID, указанный в разделе **NextGIS ID on-premise** (см. :numref:`ngidop_guid`). Его необходимо прописать в настройках учетной записи на  `my.nextgis.com <https://my.nextgis.com/myngidonpremises>`_ в разделе NextGIS ID on-premise (см. :numref:`GUID_on_my`).

.. figure:: _static/ngidop_guid.png
   :name: ngidop_guid
   :align: center
   :width: 16cm

   Идентификатор GUID в разделе NextGIS ID on-premise

.. figure:: _static/GUID_on_my.png
   :name: GUID_on_my
   :align: center
   :width: 16cm

   Идентификатор GUID в облачном аккаунте NextGIS ID
   

Использование для авторизации в приложениях
-------------------------------------------

Авторизовываться с помощью NextGIS ID on-premise умеет настольное и мобильное программное обеспечение:

* NextGIS QGIS
* NextGIS Formbuilder
* NextGIS Mobile
* NextGIS Collector


.. note::
   Для получения доступа к расширенным функциям настольного и мобильного ПО необходимо указать адрес сервера NextGIS ID в настройках настольного ПО (см. :numref:`auth_server_settings`). По-умолчанию используется публичный сервис авторизации `https://my.nextgis.com <https://my.nextgis.com>`_.

**Примечание:** во внутренней сети сервис может быть развернут по следующему адресу - `https://gis.mycompany.ru/ngid <https://gis.mycompany.ru/ngid>`_. 
Данный путь следует указывать в качестве адреса сервера авторизации. В браузере открывать следующий адрес:
* https://gis.mycompany.ru/ngid/ - профиль пользователя.

.. figure:: _static/profile_window.png
   :name: profile_window
   :align: center
   :width: 16cm

   Окно профиля пользователя
   
.. figure:: _static/auth_server_settings.png
   :name: auth_server_settings
   :align: center
   :width: 16cm

   Настройка сервера авторизации в NextGIS QGIS
 
