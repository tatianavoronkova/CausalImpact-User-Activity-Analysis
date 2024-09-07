# Анализ влияния флэшмоба на активность пользователей в социальной сети. Применение CausalImpact для оценки изменения ключевых показателей.
## Входные данные:
В приложении есть сервис ленты новостей. Команда маркетологов организовала флэшмоб в новостной ленте. Пользователи должны были сделать пост с интересным фактом о себе и добавить к нему специальный хэштег. Три поста с наибольшим числом лайков получают призы. Флэшмоб начался 2024-05-17 и длился 7 дней. Необходимо оценить, как флэшмоб повлиял на активность пользователей, используя данные о ежедневном количестве постов с хэштегом, лайков и пользователей за месяц до начала и 7 дней самого флэшмоба. 

Для этого необходимо применить метод **CausalImpact** и построить контрфактический сценарий.

## Задача: оценить разницу между предсказанными и реальными показателями активности пользователей во время флешмоба.
1. Определить ключевые метрики для оценки:
  - **Количество новых постов.** Флешмоб подразумевает размещение нового интересного поста, значит кол-во постов должно увеличится.
  - **Количество просмотров на пользователя.** Посты публикуются с хэштегом, по которому пользователь может перейти к похожим постам, и остаться в ленте дольше.
  - **Количество просмотров на пост.** Посты публикуются с хэштегом, по которому пользователь может перейти к похожим постам, значит конкурсные посты должны набирать больше просмотров.
  - **Количество лайков на пост.** Конкурс агитирует ставить лайки, чтобы выиграть и получить приз, поэтому число лайков должно увеличится.
  - **DAU.** Участники флешмоба будут заинтересованы отслеживать прогресс своих постов, скорее всего будут заходить в приложение чаще, чем обычно.
2. Проверить изменение каждой метрики методом **CausalImpact**
3. Сделать вывод

## Результат:
<image width="500" height="350" align="left" src="/images/CausalImpact_1_new_post.png" alt="Number of new posts"> 1. **Количество новых постов.** Без флешмоба среднее значение новых постов прогнозируется около 70, в то время как в действительности во время флешмоба среднее значение было около 79. Вычитая прогнозное среднее значение из фактического получаем причинно-следственный эффект 9. В относительных значениях переменная количества новых постов показала **увеличение на ~13%**.  
Полученный эффект, наблюдаемый в период флешмоба, является статистически значимым, p-value = 0.02. Вероятность получения такого эффекта случайным образом очень мала.
Но доверительный интервал полученных прогнозных значений очень широк, фактическое значение количества новых постов колеблется в рамках доверительного интервала, однозначно заявить о том, что метрика улучшилась именно в ходе флешмоба, не стоит.  

<image width="500" height="350" align="right" src="/images/CausalImpact_2_view_per_user.png" alt="Views per user"> 2. **Количество просмотров на пользователя.** Без флешмоба среднее значение просмотров на пользователя прогнозируется около 34, в то время как в действительности во время флешмоба среднее значение было около 63. Вычитая прогнозное среднее значение из фактического получаем причинно-следственный эффект 28. В относительных значениях переменная количества новых постов показала **увеличение на ~83%.**  
Полученный эффект, наблюдаемый в период флешмоба, является статистически значимым, p-value = 0.00. Вероятность получения такого эффекта случайным образом очень мала.
Доверительный интервал полученных значений довольно узкий, значит значения не слишком волатильны и плюс-минус точны. На графике видна значительная разница между прогнозными и фактическими значениями, влияние флешмоба заметно.  

<image width="500" height="350" align="left" src="/images/CausalImpact_3_view_per_post.png" alt="Views per post"> 3. **Количество просмотров на пост.** Без флешмоба среднее значение просмотров на пост прогнозируется около 2000, в то время как в действительности во время флешмоба среднее значение было около 3600. Вычитая прогнозное среднее значение из фактического получаем причинно-следственный эффект 1600. В относительных значениях переменная количества новых постов показала **увеличение на ~80%.**  
Полученный эффект, наблюдаемый в период флешмоба, является статистически значимым, p-value = 0.00. Вероятность получения такого эффекта случайным образом очень мала. В период после флешмоба фактические данные превышают прогнозные вне предела доверительного интервала 95%. 
Метрика довольно сильно коррелирует с предыдущей, поэтому выводы те же: влияние флешмоба заметно.  

<image width="500" height="350" align="right" src="/images/CausalImpact_4_like_per_post.png" alt="Likes per post"> 4. **Количество лайков на пост.** Без флешмоба среднее значение лайков на пост прогнозируется около 434, в то время как в действительности во время флешмоба среднее значение было около 791. Вычитая прогнозное среднее значение из фактического получаем причинно-следственный эффект 357. В относительных значениях переменная количества новых постов показала **увеличение на ~82%.**  
Полученный эффект, наблюдаемый в период флешмоба, является статистически значимым, p-value = 0.00. Вероятность получения такого эффекта случайным образом очень мала.
На графике видна значительная разница между прогнозными и фактическими значениями, фактические значения не пересекаются даже с доверительным интервалом прогнозных значений. Влияние флешмоба заметно.  

<image width="500" height="350" align="left" src="/images/CausalImpact_5_DAU_cov.png" alt="DAU"> 5. **DAU.** Без флешмоба среднее значение пользователей прогнозируется около 16474, в то время как в действительности во время флешмоба среднее значение было около 16052. Вычитая прогнозное среднее значение из фактического получаем причинно-следственный эффект -421. В относительных значениях переменная количества новых постов показала уменьшение на -2.56%.  
На графике видно, что значения эффекта колеблется около 0. Можно сделать вывод, что **количество пользователей во время флешмоба не увеличилось.**  
