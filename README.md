# Plagin-stackoverflow
Описание плагина IntelliJ IDEA, который обеспечивает быстрый доступ к веб-сайту StackOverflow

# Ask Question
Первое действие открывает новую страницу браузера, где мы можем задать вопрос на сайте StackOverflow (ссылка: https://stackoverflow.com/questions/ask)

Сочетание клавшиш - Cntrl+\  Cntrl+T

## Описание решения
Мы используем встроенный класс BrowserUtil, потому что он обрабатывает все нюансы открытия веб-страницы в разных операционных системах и браузерах

# My action
Второе действие открывает страницу поиска Stack Overflow и передает текст поиска в виде строки запроса

Сочетание клавшиш - Cntrl+\  Cntrl+R

## Описание решения
Сначала нам нужно собрать два значения. Первое - языковой тег, второе - текст для поиска.
Чтобы получить языковой тег, мы будем использовать интерфейс структуры программы (PSI), который отвечает за синтаксический анализ файлов и создание синтаксической и семантической модели кода. В нашем случае мы используем PSI для определения языка программирования файла:


* **PsiFile file = e.getData(CommonDataKeys.PSI_FILE);**
* **Language lang = e.getData(CommonDataKeys.PSI_FILE).getLanguage();**
* **String languageTag = "+[" + lang.getDisplayName().toLowerCase() + "]";**


Чтобы получить текст для поиска, мы будем использовать API Editor для извлечения выделенного текста на экране:


* **final Editor editor = e.getRequiredData(CommonDataKeys.EDITOR);**
* **CaretModel caretModel = editor.getCaretModel();**
* **String selectedText = caretModel.getCurrentCaret().getSelectedText();**


Также пропишем второй метод с именем **update**. Он позволит нам  отключать действие поиска, если нет выделенного текста 
