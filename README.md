# Pixel Perfect Screen
### Версия 1.0 (от 4 сентября 2024)

Swift-класс для iOS-приложения на UIKit, который позволяет добавить скриншот поверх интерфейса для упрощения верстки

### Функционал:

 - [x] Добавление скриншота поверх интерфейса на любой экран приложения
 - [x] Добавление направляющих линий с возможностью настройки их положения
 - [x] Возможность при помощи слайдеров (UISlider) двигать элементы в вашем макете - изменяя параметры элементов. Также можно выполнять любой код который будет использовать значение из слайдера.
     - Часто использую для отладки положения элементов на экране (изменения параметров констрэинтов AutoLayout)
 - [x] Возможность двигать накладываемый скрин по горизонтали
 - [x] Возможность менять непрозрачность скрина + включать / выключать его
 
 
 ## Использование:
 
 ❗️ Видео по воможностям PixelPerfectScreen - <добавить как сделаю>
 
 ### 1. Подготовка:
 
 1. Добавить на время разработки класс PIXEL_PERFECT_screen в свой проект
 
 2. Экспортировать изображение экрана, для которого надо наложить скрин из Figma или другого инструмента (желательно это делать в x2-x3 размере, который соответствует Scale Factor'у экрана для которого нарисован макет)
 
 3. Запустить симулятор у которого совпадает разрешение с разрешением под которое рисовался макет
 
 4. Добавть в Assets изображения, которые надо наложить (рекомендую называть их "PIXEL_PERFECT_<ваше название>")
 
 
 ### 2. Добавление скрина для накладывания 
 
В контроллере, который отвечает за необходимый экран в конце viewDidLoad() добавить:
 
```swift
PIXEL_PERFECT_screen.createAndSetupInstance(
    baseView: self.view, // вью на которую будет добавляться изображение
    imageName: "PIXEL_PERFECT_image_name", // имя изображения
    controlsBottomSideOffset: 0, // отступ элементов управления от низа экрана
    imageHeightDivider: 3 // scale factor с которым сохранено изображение
)
```

 ### 3. Добавление слайдеров для выполнения своего кода / доработки вьюх в реальном времени

  ```swift
// addSliderForNextInstance() надо использовать когда добавление слайдера идет перед createAndSetupInstance()
// чаще используется этот метод
PIXEL_PERFECT_screen.addSliderForNextInstance(.init(
    title: "title", // лучше давать уникальные названия
    initialValue: 10, // начальное значение слайдера
    minValue: -50, // минимальное значение
    maxValue: 100, // минимальное значение
    handler: { [weak self] sliderValue in
        // код который надо выполнить при изменении значения слайдера
    })
)

// addSliderForLastInstance() надо использовать когда добавление слайдера идет после createAndSetupInstance()
// более редкий кейс
PIXEL_PERFECT_screen.addSliderForLastInstance(.init(
    title: "title",
    initialValue: 10,
    minValue: -50,
    maxValue: 100,
    handler: { [weak self] sliderValue in
        // ...
    })
)
```

### 4. Доп. возможности (лучше смотреть в видео, когда оно будет):
 
*  Направляющие: 
    - добавляются через меню (кнопка + в левом нижнем углу)
    - удаляются и меняется их цвет при удерживании стрелочки на направляющей
    - можно их двигать удерживая их за стрелочки и перемещая
    
* Чтобы изменить положение скрина по горизонтали надо при включенном скрине делать свайп вверх/вниз по левой трети (33%) экрана
   - Установленное положение можно сбросить через меню (+)
   - Также установленное положение можно сохранить через меню (+), чтобы при следующем билде положение скрина сохранилось

* Чтобы изменить непрозрачность скрина надо при включенном скрине делать свайп вверх/вниз по правой половине (66%) экрана 
    
* Слайдеры можно скрывать на время двойным тапом на них (также можно скрывать и снова показывать через меню +)

* Можно менять положение элементов управления (слайдеров / свича / кнопки меню) перетаскивая кнопку меню (+) вверх вниз
    
    
 ### Завершение работы:

Перед релизом в поиске вбить "PIXEL_PERFECT" и удалить всё что с ним связано
 
 
 ### Цели:
 
 Хотелось сделать инструмент, который позволит без лишних зависимостей добавлять в проект функционал накладывания скрина, которые поможет в верстке макетов и чтобы код PixelPerfectScreen на как не пересекался с кодом проекта (и не мешал его работе)
 
 Также хотелось предусмотреть возможность быстрого удаления этого инструмента из кода, чтобы можно было ввести PIXEL_PERFECT в поиске и найти всё, что надо удалить перед релизом - поэтому имя класса не в CamelCase.


## License

PixelPerfectScreen is released under the MIT license.
