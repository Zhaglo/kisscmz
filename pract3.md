ЗАДАНИЕ 1. Реализовать на Jsonnet приведенный ниже пример в формате JSON. Использовать в реализации свойство программируемости и принцип DRY.

  РЕШЕНИЕ:
  ~~~
  {
    groups: [
      "ИКБО-" + std.asString(x) + "-23" for x in std.range(1, 24)
    ],
    students: [
      { name: "Иванов И.И.", group: "ИКБО-4-20", age: 19 },
      { name: "Петров П.П.", group: "ИКБО-5-20", age: 18 },
      { name: "Сидоров С.С.", group: "ИКБО-5-20", age: 18 },
      { name: "Жагло И. Д.", group: "ИКБО-10-23", age: 19 }
    ],
    subject: "Конфигурационное управление"
  }
  ~~~

ЗАДАНИЕ 2. Реализовать на Dhall приведенный ниже пример в формате JSON. Использовать в реализации свойство программируемости и принцип DRY.

  РЕШЕНИЕ:
  ~~~
  let List/length =
        https://prelude.dhall-lang.org/v21.1.0/List/length

  let groups =
        List/map Natural Text (\(i : Natural) -> "ИКБО-${Natural/show i}-23")
        (List/replicate 24 Natural/successor 0)
  
  let students =
      [ { name = "Иванов И.И.", group = "ИКБО-4-20", age = 19 }
      , { name = "Петров П.П.", group = "ИКБО-5-20", age = 18 }
      , { name = "Сидоров С.С.", group = "ИКБО-5-20", age = 18 }
      , { name = "Жагло И. Д.", group = "ИКБО-10-23", age = 19 }
      ]
  
  in  { groups = groups
      , students = students
      , subject = "Конфигурационное управление"
      }
  ~~~
