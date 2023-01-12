***Безопасно управляйте своими точечными файлами на нескольких различных компьютерах
Использование:***

`chezmoi [command]`

### доступные команды:

|cmd| discription|
---|---
`add`| Добавьте существующий файл, каталог или symlink в состояние источника|
`apply` |Обновите каталог назначения, чтобы он соответствовал целевому состоянию 
`archive`|Создайте архив tar целевого состояния
`cat`|Распечатайте целевое содержимое файла, сценария или символической ссылки
`cd`|Запустите оболочку в исходном каталоге
`chattr`|Изменение атрибутов цели в исходном состоянии
`completion`|Создать код завершения оболочки
`data`|Печать данных шаблона
`decrypt`|Расшифровать файл или стандартный ввод
`diff`|Выведите разницу между целевым состоянием и целевым состоянием
`docs`|Печать документации
`doctor`|Проверьте свою систему на наличие потенциальных проблем
`dump`|Создайте дамп целевого состояния
`edit`|Изменение исходного состояния целевого объекта
`edit-config`|Редактировать файл конфигурации
`encrypt`|Зашифровать файл или стандартный ввод
`execute-template`| Выполните заданный шаблон(ы)
`forget`| Удалить цель из исходного состояния
`git`|Запустите git в исходном каталоге
`help`|Распечатать справку о команде
`import`|Импорт архива в исходное состояние
`init`|Настройте исходный каталог и обновите каталог назначения, чтобы он соответствовал целевому состоянию
`managed`|Перечислите управляемые записи в целевом каталоге
`merge`|Выполните трехстороннее слияние между целевым состоянием, исходным состоянием и целевым состоянием
`merge-all`|Выполните трехстороннее слияние для каждого измененного файла
`purge`|Очистить конфигурацию и данные chezmoi
`re-add`|Повторное добавление измененных файлов
`remove`|Удалите цель из исходного состояния и каталога назначения
`secret`|Взаимодействие с секретным менеджером
`source-path`|Выведите путь к цели в исходном состоянии
`state`|Манипулировать постоянным состоянием
`status`|Показывать статус целей
`unmanaged`|Перечислите неуправляемые файлы в целевом каталоге
`update`|Извлеките и примените любые изменения
`verify`|Завершите работу успешно, если состояние назначения совпадает с целевым состоянием, в противном случае завершите работу неудачно

***Flags:***

|flags|discription|
---|---
`--color bool`\|`auto`|Раскрасить вывод (авто по умолчанию)
`-c, --config path`|Установить файл конфигурации (по умолчанию /data/data/com.termux/files/home/.config/chezmoi/chezmoi.toml)
`--config-format json`\|`toml`\|`yaml`|Установите формат файла конфигурации
`--debug`|Включить отладочную информацию в вывод
`-D, --destination path`|Установите каталог назначения (по умолчанию /data/data/com.termux/files/home)
`-n, --dry-run`|Не вносите никаких изменений в каталог назначения
`--force`|Внесите все изменения без запроса
`-h, --help`|помощь для chezmoi
`-k, --keep-going`|Продолжайте идти как можно дальше после ошибки
`--mode mode`|Режим
`--no-pager`|Не используйте пейджер
`--no-tty`|Не пытайтесь получить TTY для считывания паролей
`-o, --output path`|Запись вывода в путь вместо стандартного вывода
`-R, --refresh-externals`|Обновить внешний кэш
`-S, --source path`|Установите исходный каталог (по умолчанию /data/data/com.termux/files/home/.local/share/chezmoi)
`--source-path`|Укажите цели по пути к источнику
`--use-builtin-age bool`\|`auto`|Используйте встроенный возраст (авто по умолчанию)
`--use-builtin-git bool`\|`auto`|Используйте встроенный git (авто по умолчанию)
`-v, --verbose`|Сделайте вывод более подробным
`--version`|версия chezmoi
`-W, --working-tree path`|Установить каталог рабочего дерева


*Используйте `chezmoi [command] --help` для получения дополнительной информации о команде.*

