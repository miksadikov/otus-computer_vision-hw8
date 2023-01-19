# курс [OTUS Computer Vision](https://otus.ru/lessons/cv/)

## Задание №8: "Использование Facial Landmarks в качестве Feature Estimator".

Пошаговая инструкция (пайплайн) выполнения домашнего задания:
- Выберите Facial Detector по вкусу.
- Выполните Face Alignment.
- На это натравите Facial Landmarks Detector по выбору.
- На этом обучите классификатор на предпочитаемом датасете.
 
Итоговый пайплайн должен выглядеть так:
Facial Detector --> Face Alignment --> Facial Landmarks Detector --> Классификатор

Что здесь должно происходить:
- берем картинку
- находим на ней лицо (и вырезаем)
- выравниваем с помощью alignment'а
эти три пункта выполняем с помощью [Google MediaPipe Face Mesh](https://google.github.io/mediapipe/solutions/face_mesh.html)
далее:
- это выравненное лицо отдаем Facial Landmarks Detector (тоже из MediaPipe) и получаем разметку,
- эту разметку скармливаем классификатору

В качестве классификатора воспользуемся методом k-ближайших соседей. Часть кода взята из задания №9: [Face recognition](https://github.com/miksadikov/otus-computer_vision-hw9). Мы будем классифицировать выражение лица (эмоции).

В качестве датасета я взял [CK48+](https://www.kaggle.com/datasets/shawon10/ckplus), черно-белые фото, 48х48 пикселей, 7 эмоций.

Текст, что написан выше, полностью отражен в ноутбуке Otus_CV_HW8_EmotionsRecognition1.ipynb.

В ноутбуке Otus_CV_HW8_EmotionsRecognition2.ipynb я сделал несколько по другому:

в качестве Facial Detector - Face Alignment снова взял MediaPipe, но для классификации использовал нейросеть MobileNet v3. В процессе инференса сначала на фото натравливаю MediaPipe и после этого выполняю predict().
