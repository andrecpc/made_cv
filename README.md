# made_cv

Ноутбук по соревнованию https://www.kaggle.com/c/made-thousand-facial-landmarks/overview 
Результат - 34 место.

Работа велась в колабе, поэтому при локальном запуске придется закомментировать часть строк, соответствующие комментарии встречаются по ходу ноутбука.

За основу брался бейзлайн https://github.com/BorisLestsov/MADE/tree/master/contest1/unsupervised-landmarks-thousand-landmarks-contest 
Но были некоторые изменения:

1. С помощью библиотеки albumentations на основе части картинок из трейна генерировались новые 40.000 картинок с трансформациями на основе поворотов, масштабирования и сдвигов. Новые картинки добавлялись в папку с картинками трейна, также создавался дополнительный файл dop1.csv (аналогичен landmarks.csv) для новых картинок.
2. Обучение велось практически на всем трейне (TRAIN_SIZE = 0.995) и на новых 40к картинок.
3. При обучениии намеренно переобучал модель, если при каждой эпохе loss на трейне снижался, веса модели пересохранялись. Намеренно выбрал переобучение, так как такой подход показывал неплохой результат и картинок было очень много.
4. Вместо модели из бейзлайна брал resnext50_32x4d с батчем 256.
5. Во время обучения в зависимости от номера эпохи менял learning rate.
6. Для получения имеющегося результата пришлось трижды дообучать модель, комменты про это есть в ячейке тренировки.

Это все действия, которые принесли максимальный скор.

Ссылка на ноутбук на колабе https://colab.research.google.com/drive/1Nl9hgfH6bWFeoF3eE_22NlYNChz003Wb

Ссылка на файл с весами https://drive.google.com/file/d/13MyujEo6dHhmYYnWUZo1MifR7RU-eVKj/view , если надо будет проверить работоспособность кода. Оригинального файла с весами, благодаря которому получен итоговый скор, не осталось, так как файл весов перезаписывался(((

За время контеста пробовал и другие легкие модели, разные значения гиперпараметров, кросс-валидацию, стандартные трансформации, другие оптимизаторы, изменения lr  в течение эпохи, искал дубли картинок в датасетах. Хотелось проверить более громоздкие модели и в итоге сделать ансамбль, но мощностей не хватало и колаб работал нестабильно.

В начале соревнования написал заметку о загрузке данных https://www.kaggle.com/c/made-thousand-facial-landmarks/discussion/143089

![скрин1](https://github.com/andrecpc/made_cv/blob/master/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA_%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0_051220_035437_PM.jpg)
![скрин2](https://github.com/andrecpc/made_cv/blob/master/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA_%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0_051220_035514_PM.jpg)
