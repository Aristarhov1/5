# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #5 выполнил:
- Аристархов Никита Михайлович
- РИ212702
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | # | 20 |
| Задание 3 | # | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

## Цель работы
Узнать об основах машинного обучения и его роли в экономике.

## Задание 1
### Измените параметры файла. yaml-агента и определить какие параметры и как влияют на обучение модели
Ход работы:
- Открыть проект на Unity, добавить в него MlAgenta, после чего настроить его через консоль.
- Создать несколько арен в Unity, после чего запустить обучение
- Изменять параметры в Economic.yaml для достижения лучшей эффективности
- После несколькоих прогонов я определил для себя что улучшить эффективность можно либо сдвинув в большую сторону кол-во шагов, либо увеличив "силу" обучения

```c#
behaviors:
  Economic:
    trainer_type: ppo
    hyperparameters:
      batch_size: 1024
      buffer_size: 10240
      learning_rate: 3.0e-4
      learning_rate_schedule: linear
      beta: 1.0e-2
      epsilon: 0.2
      lambd: 0.95
      num_epoch: 3      
    network_settings:
      normalize: false
      hidden_units: 128
      num_layers: 2
    reward_signals:
      extrinsic:
        gamma: 0.99
        strength: 1.0             //сила обучения
    checkpoint_interval: 500000
    max_steps: 750000             //максимальное кол-во шагов
    time_horizon: 64
    summary_freq: 5000
    self_play:
      save_steps: 20000
      team_change: 100000
      swap_steps: 10000
      play_against_latest_model_ratio: 0.5
      window: 10
```

## Выводы

Системы машинного обучения позвоялют сделать игру более интересной для игроков. Так же она пзволяет регулировать экономическую систему в некоторых играх, но некоторые игры всё же требуют ручной настройки экономической модели
