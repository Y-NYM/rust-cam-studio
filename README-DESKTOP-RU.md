# Rust Cam Studio 0.5.1

Нативный интерфейс Windows/macOS для общей обработки Rust Cam.
Android-интерфейс сохранён отдельно по cfg(target_os="android").

Desktop: большое изменяемое окно, каталог камер и поиск, фоновые превью,
EV/WB/насыщенность/зерно, кадрирование, правильная композиция Inst-рамок,
JPEG/PNG, двойная экспозиция двух импортов, история файлов, нативные диалоги,
перетаскивание, Ctrl/Cmd+O/S и Shift+S, съёмка по Enter, одинаковая зеркальность превью/экспорта. Установка Windows и ярлыков: desktop/install-windows.ps1 -Executable <путь к EXE>. Веб-камера использует Media Foundation /
AVFoundation через nokhwa. Запись видео остаётся Android-функцией.

Сборка Windows: powershell -ExecutionPolicy Bypass -File build-windows.ps1
Сборка на Mac: bash build-macos.sh (Rust и Xcode Command Line Tools).
Сборка Android: powershell -ExecutionPolicy Bypass -File build-apk.ps1
Для Android нужен прежний signing/dazz-local.keystore; ключ не входит в архив.
Android cdylib теперь создаётся явным cargo rustc --crate-type cdylib.
Тесты: cargo test -p dazz-core -p dazzcam --lib --locked

Командный экспорт: RustCamStudio.exe --render input.jpg --output result.png --camera instsqc
Исходное разрешение доступно в GUI; PNG без потерь, JPEG quality 94.
Original на desktop нейтрален до ручной коррекции, импорт не грейдится повторно.

Windows проверен запуском настоящего GUI в трёх размерах/состояниях через
снимки renderer и отдельными запусками бинарника для JPEG/PNG.
Сервис управления окнами не отвечал, поэтому ручные щелчки системных диалогов
не подтверждены. Камера HP Wide Vision HD проверена на Windows: поток 1280×720, остановка, повторное включение и сохранение снимка через Enter. Добавлен выбор зеркальности, единый для превью и экспорта.
macOS: Universal2 arm64+x86_64, SDK 11.3, deployment target 11.0,
ad-hoc подпись и проверка rcodesign. Запуск на Mac не проверен.
Нет Developer ID / Apple notarization. Для публичной подписанной поставки
нужны данные владельца; текущая сборка локальная.

Все числовые рецепты плёнок, WB и blend 50/50 приближённые. Jitter использует
chroma/scanlines, Halation — bloom, точные Dazz-операции не восстановлены.
UI не отправляет фото в сеть. Прежние ограничения Android — в Build-report.txt.
