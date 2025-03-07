# Распознаватель текста с pdf-документов

<h4>Установка библиотек</h4>

```
pip install -r requirements.txt
```

<hr>

<h4>Реализация.</h4>
<ul>
    <li>
        Программа реализовывалась на Windows.
    </li>
    <li>
        В ней доступно 3 разных способа распознавания: через Tesseract, через Easyocr и через снятие текстового слоя (для pdf, у которых текст можно выделить при попытке скопировать его).
    </li>
</ul>
<hr>

<h4>Установка вручную и настройка для Tesseract.</h4>
<b>Перед запуском распознавания через Tesseract необходимо дополнительно установить и настроить 2 программы:</b>

<ol>
  <li>
    Установка Tesseract
    <ul>
      <li>Необходимо перейти по <a href="https://tesseract-ocr.github.io/tessdoc/Installation.html">ссылке</a> и скачать к себе Tesseract.</li>
      <li>Без этого распознаватель текста работать не будет.</li>
      <li>Для Windows Tesseract можно скачать <a href="https://github.com/UB-Mannheim/tesseract/wiki">отсюда</a>.</li>
      <li>Во время установки не забывайте выбрать языки, которые Вам будут нужны. Это настраивается в "Additional language data".</li>
      <li>Далее необходимо в переменных среды PATH добавить новую переменную: прописать путь к папке, в которую Вы установили ранее скачанный Tesseract.</li>
    </ul>
  </li>
  <li>
    Конвертор pdf в image
    <ul>
      <li>После этого необходимо скачать <a href="https://github.com/oschwartz10612/poppler-windows/releases">конвертор pdf в image</a> (Poppler) и разархивировать её к себе.</li>
      <li>Затем необходимо в переменную среды PATH по аналогии добавить новую переменную: прописать путь к папке, в которой лежит Poppler, но в этот раз к bin, которая находится где-то в этой папке.</li>
    </ul>
  </li>
  <li>После прописания в PATH желательно перезагрузить устройство, чтобы все сработало.</li>
</ol>

<ul>
    <li>
        При установке библиотек для Tesseract может выдаваться в терминале что-то по типу "A new release of pip is available:", тогда просто введите предложенную команду для обновления pip.
    </li>
    <li>
        Команды для обоих способов также написаны в верху файлов.
    </li>
</ul>
<hr>


<h4>Языки.</h4>

<ul>
<li>
Чтобы узнать (в Tesseract) обозначение языков, можно ввести в терминале команду:

```
tesseract --list-langs
```
    
</li>
<li>Языки (в Tesseract) также можно комбинировать, вот пример, как это можно сделать: "eng+rus"</li>
<li>В Easyocr можно посмотреть языки здесь: https://www.jaided.ai/easyocr/</li>
<li>Языки (в Easyocr) можно комбинировать, добавив в список несколько языков</li>
<li>При распознавании с текстовым слоем (text_from_layer_pdf.py) язык передавать не нужно</li>
</ul>




<hr>
<h4>Автоматическая установка Tesseract.</h4>
<ul>
    <li>
        Если вы хотите начать установку Tesseract с помощью программы, то Вы можете это сделать, запустив от имени администратора файл auto_install_tesseract.py.
    </li>
    <li>
        Не забудьте настроить нужные языки в процессе установки.
    </li>
    <li>
        <b>После установки Ваше устройство будет перезагружено.</b>
    </li>
</ul>


<hr>
<h4>Easyocr.</h4>
<ul>
    <li>
        Перед запуском распознавания через easyocr необходимо скачать <a href="https://github.com/oschwartz10612/poppler-windows/releases">конвертор pdf в image</a> и следовать рекомендациям для Poppler про путь<br>(2 пункт про "Установка вручную и настройка для Tesseract", Poppler необходимо везде настроить одинаково).
    </li>
    <li>
        Для использования GPU в распознавании от ошибки (Neither CUDA nor MPS are available - defaulting to CPU. Note: This module is much faster with a GPU.) я ввел это в терминал:

```
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
```
    
</li>


</ul>
<hr>
<h4>Запуск программы.</h4>
<ul>
    <li>Программа запускается через терминал, ниже примеры запусков</li>
    <li>python text_from_tesseract.py --languages rus eng --path test_files/file_1.pdf --first_page 1 --last_page 5</li>
    <li>python text_from_easy_ocr.py --languages ru en --path test_files/file_1.pdf --first_page 1 --last_page 5</li>
    <li>python text_from_layer_pdf.py --path test_files/file_1.pdf --first_page 1 --last_page 5</li>
    <br>
    <li>--languages: языки в документе, которые надо распознать (обязательно к передаче в программу, если не запускаете text_from_layer_pdf.py)</li>
    <li>при запуске text_from_layer_pdf.py языки передавать не нужно</li>
    <li>--path: путь к pdf файлу (обязательно к передаче в программу)</li>
    <li>--first_page: первая страница, с которой начать распознавание текста (необязательно к передаче, по дефолту стоит первая страница)</li>
    <li>--last_page: последняя страница, до которой распознавать текст (включительно), (необязательно к передаче, по дефолту стоит последняя страница в документу)</li>
    <br>
    <li>Не забывайте про разницу обозначения языков для способов распознавания через tesseract и easyocr</li>
</ul>
<hr>