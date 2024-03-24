# Как запустить свой первый портал

<a id = "anchor-1"></a>

## Предварительная подготовка

1. Регистрируемся в [GitHub](https://github.com/). 

2. Создаем свой первый проект. Это можно сделать сразу после регистрации или создать позже.

3. Устанавливаем Git: https://git-scm.com/download/win.

4. Устанавливаем Python, например последнюю версию: https://www.python.org/downloads/release/python-3121/. Пролистайте в самый низ и выберите версию для вашей ОC. Для пользователей MacOS, можно скачать все следующей командой:

	```
	brew install python
	```

5. Для самых стойких — установить Docker: https://www.docker.com/get-started/. С помощью докера мы будем автоматизировать выкладку обновлений контента.

6. Перезапустите компьютер после установки всех компонент.

7. Проверьте, что Git и Python успешно установились:

	```
	git --version
	git version 2.40.1.windows.1
	   
	python --version
	Python 3.11.1
	   
	pip --version
	pip 22.3.1 from C:\Users\User\AppData\Local\Programs\Python\Python311\Lib\site-packages\pip (python 3.11)
	```

## Первые шаги

Мы будем использовать язык разметки Markdown и движок MkDocs для генерации статического контента.

1. Открываем терминал.

2. Устанавливаем MkDocs локально:

	```
	pip install mkdocs
	```

3. Проверяем, что все установилось:

	```
	mkdocs --version
	mkdocs, version 1.5.3 from C:\Users\User\AppData\Local\Programs\Python\Python311\Lib\site-packages\mkdocs (Python 3.11)
	```

4. Создаем свой первый проект в текущей директории:

	```
	mkdocs new my-project
	```

5. Переходим в директорию с проектом:

	```
	cd my-project
	```

6. Собираем и запускаем локально портал:

	```
	mkdocs serve
	```

   В конце, в результате выполнения команды можно получить ссылку по которой доступен результат сборки портала:

	```
	INFO    -  Building documentation...
	INFO    -  Cleaning site directory
	INFO    -  Documentation built in 0.19 seconds
	INFO    -  [16:00:36] Watching paths for changes: 'docs', 'mkdocs.yml'
	INFO    -  [16:00:36] Serving on http://127.0.0.1:8000/
	```

7. Копируем ссылку и вставляем в адресную строку.

## Наводим красоту

Практически все визуальные настройки выполняются в рамках файла mkdocs.yml. Изначально он состоит лишь из одной строчки:

```
site_name: My Docs
```

Для MkDocs есть множество различных тем, плагинов и расширений. Самая популярная тема для MkDocs c активной поддержкой и постоянным развитием — это MkDocs Material: https://squidfunk.github.io/mkdocs-material/. Сделаем наш портал в такой же теме.

1. Установим тему Material:

  ```
  pip install mkdocs-material
  ```

2. Откроем файл mkdocs.yml и подключим ее к нашему проекту:

  ```
  theme:
  	name: material # основная тема, которую используем, https://squidfunk.github.io/mkdocs-material/
  ```

3. Пересоберем портал:

  ```
  mkdocs serve
  ```

4. Нам нужно добавить новый документ на наш портал и при это указать его в навигационном меню. Для этого в файле mkdocs.yml нужно создать новую секцию:

  ```
  nav:
  ```

5. Теперь скачайте из Телеграмма файлик `my-first-docs-portal.md`. И перенесите его в папку docs в вашем проекте.

6. Добавим инструкцию на портал:

   ```
   nav:
   	- Как создать свой первый портал?: my-first-docs-portal.md
   ```

7. Добавим группирующий раздел и перенесем навигационную панель наверх.

   ```
   nav:
   	- HowTo:
   		- Как создать свой первый портал?: my-first-docs-portal.md
   	- FAQ:
   theme:
   	name: material # основная тема, которую используем, https://squidfunk.github.io/mkdocs-material/
   	features:
   		- navigation.tabs
   		
   ```

8. Заменим логотип на нашем портале:

```
theme:
	name: material # основная тема, которую используем, https://squidfunk.github.io/mkdocs-material/
	logo: VK_WorkSpace_logo.svg # относительный путь к лого, который отображается на портале и на титуле дока, в колонтитулах дока, обязательно svg
```

1. Поменяем цвета портала на корпоративные. Для этого нужно внутри папки docs нужно создать файл material-styles.css и указать путь до него в mkdocs.yml:

  ```
  extra_css:
  	- material-styles.css
  ```

     А внутри файла material-styles.css укажем стили для шапки нашего портала:
    
     ```
     .md-header {
     --md-primary-fg-color: #FFFFFF;
     --md-primary-bg-color: #000000;
     }
     ```



Итоговый `mkdocs.yml`:

```
site_name: My Docs
nav:
    - HowTo:
        - Как создать свой первый портал?: index.md
    - FAQ:
        - Вопрос-ответ: my-first-docs-portal.md
theme:
    name: material # основная тема, которую используем, https://squidfunk.github.io/mkdocs-material/
    logo: VK_WorkSpace_logo.svg # относительный путь к лого, который отображается на портале и на титуле дока, в колонтитулах дока, обязательно svg
    features:
        - navigation.tabs
extra_css:
    - material-styles.css
```



Рекомендуемые инструменты:

1. Плагин для загрузки видео на портал:

	```
	plugins:
		- mkdocs-video:
			is_video: True #изменение тега для видео на конечной странице html (было <iframe>, стало <video>, когда true)
			#video_type: mpeg #- если формат видео не mp4 (по умолчанию), а другой. Этот параметр будет работать только с <video> тегом ( is_video: True)
			#video_autoplay: True # автовоспроизведение видео. Этот параметр будет работать только с <video> тегом ( is_video: True)
			#video_loop: False # зацикливание видео. Этот параметр будет работать только с <video> тегом ( is_video: True)
			video_muted: True # должно ли видео быть на мьюте. Этот параметр будет работать только с <video> тегом ( is_video: True)
			video_controls: True # отображение элементов управления видео. Этот параметр будет работать только с <video> тегом ( is_video: True)
			css_style:
			  width: "100%" #изменение ширины видео по дефолту
	```

2. Расширение, которое делает красивые примечание:

	```
	markdown_extensions:
		- admonition # примечания (коллауты), описание https://squidfunk.github.io/mkdocs-material/setup/extensions/python-markdown/#admonition и https://python-markdown.github.io/extensions/admonition/
	```

3. Расширение, которое позволяет переиспользовать одинаковые части документации:

	```
	markdown_extensions:
		- pymdownx.snippets # Расширение Snippets добавляет возможность встраивать в документ содержимое из произвольных файлов, включая другие документы или исходные файлы
	```

## Начинаем работать с Git

Чтобы сохранять, версионировать и запускать портал нам понадобится GitLab/GitHub. Сначала нам нужно склонировать репозиторий, который мы создавали на шаге [Предварительная подготовка](#anchor-1).

1. Склонируем репозиторий в любое удобное место, но не в папку с нашим порталом. 

	```
	PS C:\Users\User\Desktop> git clone https://gitlab.com/nikitasgroup1/my-first-docs-portal
	```

2. В моем случае, я клонировал на рабочий стол и у меня появилась папка с названием репозитория. Теперь нужно перенести все содержимое папки my-project внутрь новой папки.

3. Перейдем внутрь папки репозитория.

	```
	cd my-first-docs-portal
	```
	
3. Собираем наш первый коммит:

	```
	git add . --all
	git commit -m "Наш первый портал"
	```
	
	Итог
	
	```
	[main 88fd875] Наш первый портал
	 5 files changed, 206 insertions(+)
	 create mode 100644 docs/VK_WorkSpace_logo.svg
	 create mode 100644 docs/index.md
	 create mode 100644 docs/material-styles.css
	 create mode 100644 docs/my-first-docs-portal.md
	 create mode 100644 mkdocs.yml
	```
	
3. Отправим изменения в репозиторий на сервер GitHub'а:

	```
	git push -uf origin main
	```
	
	Итог:
	
	```
	Перечисление объектов: 12, готово.
	Подсчет объектов: 100% (12/12), готово.
	При сжатии изменений используется до 8 потоков
	Сжатие объектов: 100% (10/10), готово.
	Запись объектов: 100% (10/10), 11.02 КиБ | 11.02 МиБ/с, готово.
	Всего 10 (изменений 0), повторно использовано 0 (изменений 0), повторно использовано пакетов 0
	To https://github.com/Recours/DocsPortal.git
	   e7a1c28..c9db308  main -> main
	branch 'main' set up to track 'origin/main'.
	```
	
	

